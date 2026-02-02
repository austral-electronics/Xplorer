# 📚 TABLE OF CONTENTS
- **[1 - Create connection for a Quectel EM060K-GL 4G Modem](#1)**
- **[2 - Switch a Quectel EM060K-GL modem to QMI mode](#2)**
- **[3 - SIM8230G - 5G RedCap Modem on ECM mode](#1)**
---

# 1 - Create connection for a Quectel EM060K-GL 4G Modem<a name="1"></a>

### 1️⃣ Unlock the SIM card
With ModemManager you ask:
```
mmcli -L
```
you should see:
>/org/freedesktop/ModemManager1/Modem/0 [Quectel] EM060K-GL

this reply give you that the modem on slot: **0**

then settings:
```
mmcli -m 0
```
Unlock the SIM PIN
Run: (Replace 0000 with your actual SIM PIN)
```
sudo mmcli -i 0 --pin=0000
```
After unlocking, check again:
```
mmcli -m 0
```
You should now see:
>state: enabled
>lock: none

### 2️⃣ Enable the modem
```
sudo mmcli -m 0 --enable
```

you must check as well that you ports cdc-wdm0 and wwan0, that means the module is in QMI mode which is good, otherwise go to paragraph **[2 - Switch a Quectel EM060K-GL modem to QMI mode](#2)**:
>ports: cdc-wdm0 (qmi), wwan0 (net)

Check bearer:
```
mmcli -m 0 | grep Bearer
```
You’ll see something like:
>Bearer paths: /org/freedesktop/ModemManager1/Bearer/1

number 1 at the end of the path means that bearer is in slot 1.
Enable it:
```
sudo mmcli -b 1 --connect
```
Check it is connected:
```
sudo mmcli -b 0
```
>Status     |   connected: yes

### 3️⃣ Create connection with Network Manager
get device list:
```
nmcli device
```
you should have:
>cdc-wdm0       gsm       disconnected            --  

if device cdc-wdm0 haven't a connection create it like this:
enter your APN, here for the example the APN is "sl2sfr"  .
⚠️ By creating the connection that creates the bearer, this is the step where you enter the APN.
```
sudo nmcli connection add \
  type gsm \
  ifname wwan0 \
  con-name quectel \
  apn sl2sfr \
  ipv4.method auto \
  ipv6.method auto
```
Bring the connection up:
```
sudo nmcli connection up quectel
ip addr show wwan0
```
🚀check the connection:
```
ping -I wwan0 8.8.8.8
```
and the DNS:
```
ping -I wwan0 google.com
```


# 2 - Switch a Quectel EM060K-GL modem to ECM mode<a name="2"></a>

If you only want ECM data and don’t need MM’s SIM/AT management:
```
sudo systemctl stop ModemManager
sudo systemctl disable ModemManager
```
Then reboot:
```
sudo reboot now
```

from dmesg you should see usbUSB ports:
```
dmesg | grep ttyUSB
```
With the Xplorer you should have four: ttyUSB 4 -> 7

and if with 
```
lsusb -t
```
you don't see 
>Driver=qmi_wwan
>Driver=cdc_wdm

that mean your modem is not in QMI mode, let's crack on


## 💳 Check SIM status:
```
AT+CPIN?
```
Expected:
>+CPIN: READY
>OK

If you get:
* SIM PIN → PIN not entered
* SIM NOT INSERTED
* ERROR

If PIN is needed:
```
AT+CPIN="0000"
```
Wait ~5–10 seconds, then re-check:
```
AT+CPIN?
```
Wait until you see all these messages:
>+CPIN: READY
>SMS DONE
>PB DONE

```
AT+QCFG="usbnet"
```
```
AT+QCFG="usbnet",0
```
```
AT+CFUN=1,1
```
get usbcfg settings:
```
AT+QCFG="usbcfg"
```
You should have something like this:
>+QCFG: "usbcfg",0x2c7c,0x030B,1,0,1,1,0,0,0

Let’s decode it field-by-field:

usbcfg,
VID,   PID,
diag, nmea, at_port, modem, rmnet, adb, uac


So yours is:

| Field | Value | Meaning|
| ----------- | ----------- | ----------- |
| diag | 1|  enabled| 
| nmea| 1 | enabled | 
| at_port | 1 | enabled| 
| modem | 1 | ❌ PPP modem interface ENABLED| 
| rmnet | 0 | ❌ QMI (rmnet) DISABLED| 
| adb | 0 | disabled| 
| uac | 0 | disabled| 

👉 This explains everything:

Linux only sees option (serial)

* No cdc-wdm
* No qmi_wwan
* No /dev/cdc-wdm*

Even though:

usbnet = 0 (QMI mode selected internally)

⚠️ usbnet=0 does NOT automatically enable rmnet
You must explicitly enable it in usbcfg.

✅ The correct QMI USB composition (what we want)

We want:

| Field | Value|
| ----------- | ----------- |
| diag | 1|
| nmea | 1|
| at_port | 1|
| modem | 0 ← disable PPP modem|
| rmnet | 1 ← enable QMI|
| adb | 0|
| uac | 0|

Set the correct USB composition:
```
AT+QCFG="usbcfg",0x2c7c,0x030B,1,1,1,0,1,0,0
```
⚠️ If you mistype VID or PID, the command is ignored silently — yours must be exactly the same number that AT+QCFG="usbcfg" reply. in our example it is : 0x2c7c,0x030B. your can change

2️⃣ Hard reboot the modem (mandatory)
```
AT+CFUN=1,1
```
3️⃣ FULL HOST POWER CYCLE (not optional)

This is critical on Quectel:
```
sudo poweroff
```

⚠️ After reboot we are in a half-switched USB composition state, we now have exactly two GSM serial ports. AT port should now be accessible on another port (usally 5)
 
test if you are in QMI mode:
```
ls /dev/cdc-wdm*
```
if you still don't see:
>/dev/cdc-wdmx

that mean the QMI mode is not attached to a valid PID

✅ Test the QMI mode with your PID
Add the PID to qmi_wwan.This does not change modem firmware.
It only tells Linux: “this PID supports QMI”.
Load qmi_wwan:
```
sudo modprobe qmi_wwan
```
Bind your PID manually, put your VID and PID number, in our example it is : 0x2c7c,0x030B (Use lowercase hex — kernel expects that.)
```
echo 2c7c 030b | sudo tee /sys/bus/usb/drivers/qmi_wwan/new_id
```
test if QMI mode is activated:
```
ls /dev/cdc-wdm*
```
You should see:
>/dev/cdc-wdmx

To make it permanentely, Change PID to a known Quectel QMI PID. 
This does not change radio behavior — only USB ID. This is the cleanest and most future-proof solution. Linux already knows how to bind QMI for some Quectel PIDs.
One very common, safe one is:
>PID = 0x0125

Change USB PID (AT command)

In minicom (AT port still works on ttyUSB4/5):
```
AT+QCFG="usbcfg",0x2C7C,0x0125,1,1,1,0,1,0,0
```
```
AT+CFUN=1,1
```

⚠️ Then manually recycle the power supply.

🧹 STEP 1 — Disconnect and delete all bearers
List bearers
mmcli -m 0


You’ll see something like:

Bearer paths: /org/freedesktop/ModemManager1/Bearer/1

Disconnect bearer
sudo mmcli -b 1 --disconnect

Delete bearer
sudo mmcli -b 1 --delete


📌 If there are multiple bearers, repeat for each.

Verify
mmcli -m 0 | grep Bearer

Expected:
Bearer paths: none

# 3 - SIM8230G - 5G RedCap Modem  on ECM mode<a name="1"></a>

⚠️ You can't use ModemManager on ECM mode

With ModemManager you ask:
```
mmcli -L
```
you can find a modem on slot: **0**:
>/org/freedesktop/ModemManager1/Modem/0 [SIMCOM INCORPORATED] SIMCOM_SIM8230G

Get settings:
```
mmcli -m 0
```
You can see:
>drivers: option, cdc_ether
>ports: ttyUSB6 (at), usb0 (net)

#### 🔍 What ModemManager is telling you

This means:
* The kernel created usb0 (ECM network interface)
* ModemManager knows usb0 exists
* ModemManager classifies usb0 as a net port belonging to the modem

But this does not mean NetworkManager will manage it.

#### 🔍 Why NetworkManager does NOT show usb0
NetworkManager hides usb0 because:

1️⃣  <u>ModemManager “owns” the modem</u> 

When ModemManager claims a modem, NetworkManager assumes:
>“ModemManager will handle data connections.”

So NetworkManager refuses to manage usb0, even though it exists.

This is exactly what you see:

* ModemManager sees usb0
* NetworkManager does not see usb0
* NetworkManager only shows ttyUSB6 as a GSM modem device

2️⃣ <u>ECM interfaces are not modem interfaces</u>

ECM is a simple Ethernet-over-USB link.
But NetworkManager will only manage it if:

* ModemManager is not managing the modem
* NetworkManager is allowed to manage Ethernet-like interfaces

Right now, ModemManager is still claiming the modem, so NM hides usb0.

#### ❌ Disable ModemManager entirely

If you only want ECM data and don’t need MM’s SIM/AT management:
```
sudo systemctl stop ModemManager
sudo systemctl disable ModemManager
```
Then reboot:
```
sudo reboot now
```
Then NM will manage usb0 normally.

## 💻Connect with terminal 
#### Check the SIM8230G is mounted
```
lsusb
```
you should see, driver must be 'cdc_ether':
>Bus 001.Port 001: Dev 001, Class=root_hub, Driver=dwc2/1p, 480M
    |__ Port 001: Dev 002, If 0, Class=Vendor Specific Class, Driver=option, 480M
    |__ Port 001: Dev 002, If 1, Class=Vendor Specific Class, Driver=option, 480M
    |__ Port 001: Dev 002, If 2, Class=Vendor Specific Class, Driver=option, 480M
    |__ Port 001: Dev 002, If 3, Class=Communications, Driver=cdc_ether, 480M
    |__ Port 001: Dev 002, If 4, Class=CDC Data, Driver=cdc_ether, 480M

on Xplorer you have:
* ttyUSB4 is diagnostic
* ttyUSB5 is NMEA/GNSS
* ttyUSB6 is AT command port
* ttyUSB7 is Secondary AT / QMI control

#### open a AT connection with the modem:
```
sudo minicom -D /dev/ttyUSB6
```
Write :
```
AT
```
You should see:
>OK

Get Details of the modem:
```
AT+SIMCOMATI
```

## 💳 Check SIM status:
```
AT+CPIN?
```
Expected:
>+CPIN: READY
>OK

If you get:
* SIM PIN → PIN not entered
* SIM NOT INSERTED
* ERROR

If PIN is needed:
```
AT+CPIN="0000"
```
Wait ~5–10 seconds, then re-check:
```
AT+CPIN?
```
Wait until you see all these messages:
>+CPIN: READY
>SMS DONE
>PB DONE


## 🔧 Configure APN
Check if you already have an APN set:
```
AT+CGDCONT?
```
if there some APN set you should see:
>+CGDCONT: 1,"IP","","0.0.0.0",0,0,0,0,,,,,,,,,,"",,,,0
+CGDCONT: 2,"IPV4V6","ims","0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0",0,0,0,0,,,,,,,,,,"",,,,0
+CGDCONT: 3,"IPV4V6","sos","0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0",0,0,0,1,,,,,,,,,,"",,,,0
+CGDCONT: 4,"IPV4V6","sl2sfr","0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0",0,0,0,0,,,,,,,,,,"",,,,0

Correct way forward (do NOT use PDP1). IP, ims and sos **must not** be overwrited, then to create your user PDP number must be higher or equal to slot 4. ask your SIM card provider what is the APN name.

If your APN is not set :
```
AT+CGDCONT=4,"IPV4V6","your.apn.here"
```
Example: For Auchan Telecom (France). Auchan Telecom APN is typically: "sl2sfr"
```
AT+CGDCONT=4,"IPV4V6","sl2sfr"
```


## 👉 Activate the existing APN (CID 4)
Run:
```
AT+CGACT=1,4
```
Then verify:
```
AT+CGACT?
```
In the list you should see:
>+CGACT: 4,1
>OK

If that succeeds, the LTE data session is up.
## 🚀 Start SIMCom data routing
On SIM82xx / SIM7600 family, CGACT alone is often not enough for ECM.
Run one of these (depends on firmware):
```
AT+NETOPEN
```
If that errors, try:
```
AT+CMNETSTART
```

Check status:
```
AT+NETOPEN?
```
Expected:
>+NETOPEN: 1
This step is what enables packet forwarding from ECM to LTE.

Check LTE/5G registration (this is critical)
```
AT+CEREG?
```
ou need one of these:
* 1 (home)
* 5 (roaming)

If you get 0, 2, or 3, PDP activation will fail.

Check system state:
```
AT+CPSI?
```
You should see:
* LTE or NR5G
* Valid band
* Not NO SERVICE


## 🛠️ 2. Create a NetworkManager connection for ECM (usb0)

check if there already a connection:
```
nmcli connection && nmcli device
```
you may see something like this:
>xplr@xplorercm5:~ $ nmcli connection
>NAME                UUID                                  TYPE      DEVICE 
>wired_eth0          5d6d8f2d-f3d9-40b7-8957-2939e2bfa0d3  ethernet  eth0   
>Wired connection 1  bf167c0f-e50f-3ab0-87f5-976f56ab7b0e  ethernet  usb0   
>lo                  65257f52-5a9a-4514-8997-5f1350f02ed8  loopback  lo     

>xplr@xplorercm5:~ $ nmcli device
>DEVICE         TYPE      STATE                   CONNECTION         
>eth0           ethernet  connected               wired_eth0         
>usb0           ethernet  connected               Wired connection 1 
>lo             loopback  connected (externally)  lo                 
>wlan0          wifi      disconnected            --                 
>p2p-dev-wlan0  wifi-p2p  disconnected            --                 
>can0           can       unmanaged               --                 
>can1           can       unmanaged               -- 

If there is a connection that already using **usb0**, delete it (here it is'Wired connection 1') :
```
sudo nmcli connection down 'Wired connection 1'
sudo nmcli connection delete 'Wired connection 1'
```
 
Then create a new one:
```
sudo nmcli connection add type ethernet ifname usb0 con-name simcom-ecm
```
Then enable DHCP:
```
sudo nmcli connection modify simcom-ecm ipv4.method auto ipv6.method ignore
```
Bring it up:
```
sudo nmcli connection up simcom-ecm
```
If the modem has already opened the data session internally, you should get an IP:
```
ip addr show usb0
```
You want the usb0 interface get an IP address something like:
```
inet 10.x.x.x/24
```
Then test the connection:
```
ping -I usb0 8.8.8.8
```
and test DNS:
```
ping -I usb0 google.com
```

## 📌 TIPS
#### 1️⃣  Reset the modem:
If you need to reset the modem, this is not needed when modem come from a hardware reboot or boot up:
```
AT+CRESET=?
```
then :
```
AT+CRESET
```
After 20 seconds you may see:
>+CIPEVENT: NETWORK CLOSED UNEXPECTEDLY

and then the terminal will disconnect from the modem and come back after another 20 seconds

#### 2️⃣ Delete PDP
##### 📡 What Is a PDP Context?

A PDP context (Packet Data Protocol context) is a configuration profile used by a 4G/5G modem to establish a data session with the mobile network.
It defines how the modem connects to the operator’s packet network.

A PDP context typically contains:
* CID (Context ID)
* PDP type (IP / IPV4V6 / etc.)
* APN (Access Point Name)
* IP address allocation mode

Other network parameters

When the modem attaches to the network, it uses one or more PDP contexts to request data connectivity.

🧩 Why Are There Multiple PDP Contexts?
Modern LTE/5G networks use separate APNs for different services, for example:
* IMS → VoLTE (voice over LTE)
* SOS → emergency services
* MMS → multimedia messaging
* DATA → your main internet APN

The modem may create some of these automatically based on the SIM card’s operator.

🔒 Which PDP Contexts Cannot Be Deleted?

On SIMCom modules such as the SIM8230G, some PDP contexts are mandatory and will be recreated automatically by the firmware even if you delete them.

| CID      | APN | Purpose | Deletable? |
| ----------- | ----------- | ----------- | ----------- |
| ims      | IMS services   | Required for VoLTE | ❌ Cannot be deleted |
| sos   | Emergency services | Required by 3GPP | ❌ Cannot be deleted |

These two are part of the 3GPP specifications and are always restored by the modem.

🟡 PDP Contexts That Can Be Deleted
Any PDP context that is not IMS or SOS is optional and can be removed, for example:
* Your custom APN (e.g., sl2sfr)
* MMS APNs (e.g., mmsbouygtel.com)
* Placeholder APNs (e.g., your.apn)
* Any operator‑specific APN that you do not use

These can be deleted with:
```
AT+CGDCONT=<cid>
```
However, note:

* Some operator APNs (like MMS) may reappear until the SIM is unlocked (+CPIN: READY).
* Once the SIM is unlocked, they can usually be removed permanently.

Show PDP:
```
AT+CGDCONT?
```
you should see:
>+CGDCONT: 1,"IP","","0.0.0.0",0,0,0,0,,,,,,,,,,"",,,,0
+CGDCONT: 2,"IPV4V6","ims","0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0",0,0,0,0,,,,,,,,,,"",,,,0
+CGDCONT: 3,"IPV4V6","sos","0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0",0,0,0,1,,,,,,,,,,"",,,,0
+CGDCONT: 4,"IPV4V6","sl2sfr","0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0",0,0,0,0,,,,,,,,,,"",,,,0
+CGDCONT: 5,"IPV4V6","mmsbouygtel.com","0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0",0,0,0,0,,,,,,,,,,"",,,,0

As long as the SIM is not unlocked, the module considers self-generated PDPs to be "protected". Unlock the SIM card:
```
AT+CPIN="xxxx"
```
Then delete your PDP (here number 4 and 5):
```
AT+CGDCONT=5
```
```
AT+CGDCONT=5
```

# 2 - SIM8230G - 5G RedCap Modem with MM<a name="1"></a>
```
mmcli -L
```
```
mmcli -m 0
```
```
sudo mmcli -i 0 --pin=0000
```
```
sudo mmcli -m 0 --create-bearer="apn=sl2sfr,ip-type=ipv4v6"
```
```
sudo mmcli -b 0 -m 0 --connect
```
```
nmcli c add type gsm ifname "*" con-name simcom apn sl2sfr
```
```
nmcli device && nmcli connection
```



