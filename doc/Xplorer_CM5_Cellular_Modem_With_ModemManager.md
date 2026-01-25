# <code style="color : BLACK">XPLORER CM5 - Configure a Cellular / Direct-To-Cell modem with Modem Manager - 🅰🆄🆂🆃🆁🅰🅻 Electronics</code>

# 📚 TABLE OF CONTENTS
- **[1 - QUECTEL EM60K-GL - 4G LTE-A Modem](#1)**
- **[2 - SIM8230G - 5G RedCap Modem](#2)**
---

# 1 - QUECTEL EM60K-GL - 4G LTE-A Modem <a name="1"></a>

The EM60K-GL is an LTE Cat 6 data modem

It supports QMI and MBIM

The Quectel must expose  QMI or MBIM mode so ModemManager can detect the modem
```
lsusb
```
You should see:
> Bus 001 Device 002: ID 2c7c:030b Quectel Wireless Solutions Co., Ltd. EM060K-GL

After correct setup, you should see one of these:
```
ls /dev/cdc-wdm*
```
Example:
> /dev/cdc-wdm0

And a network interface:
```
ip link
```
Example:
> wwan0

And then:
```
mmcli -L
```
you should see:
> /org/freedesktop/ModemManager1/Modem/0 [Quectel] EM060K-GL

if you see:
> No modems were found


Check connection works:
```
sudo qmicli -d /dev/cdc-wdm0 --device-open-proxy --uim-get-card-status
```
You should see something like:
>[/dev/cdc-wdm0] Successfully got card status Provisioning applications: Primary GW: session doesn't exist Primary 
>1X: session doesn't exist Secondary GW: session doesn't exist 
>Secondary 1X: session doesn't exist 
>Slot [1]: Card state: 'error: no-atr-received (3)' UPIN state: 'not-initialized' UPIN retries: '0' UPUK retries: '0'

this output actually answers several important questions:
✅ The kernel loaded the qmi_wwan driver
✅ /dev/cdc-wdm0 is functional
✅ The USB interface is in QMI mode
✅ Userspace ↔ modem communication is working
✅ module is detected with: QMI (cdc-wdm0)

👉 ModemManager has decided that /dev/cdc-wdm0 is an MBIM device, not QMI. But your modem is actually operating in QMI mode (as proven by qmicli).

### 🔧 Step-by-step FIX
1️⃣ We need to blacklist MBIM kernel driver
Create this file:
```
sudo nano /etc/modprobe.d/blacklist-cdc-mbim.conf
```
Add:
```
blacklist cdc_mbim
```
Save and exit.

2️⃣ Ensure QMI drivers are present
```
sudo modprobe qmi_wwan
sudo modprobe cdc_wdm
```
3️⃣ Reboot (required)
```
sudo reboot now
```
This step is not optional — USB driver binding must reset.


✅ Final verification

Now:
```
mmcli -L
```

You should finally see:

> /org/freedesktop/ModemManager1/Modem/0 [Quectel] EM60K-GL


And:
```
mmcli -m 0
```

# 2 - SIM8230G - 5G RedCap Modem <a name="2"></a>
```
sudo mmcli --scan-modems
```
```
mmcli -L
```
>/org/freedesktop/ModemManager1/Modem/0 [SIMCOM INCORPORATED] SIMCOM_SIM8230G

This feedback tells you that there is a SIM8230G modem on instance: 0

Now you can display settings of this instance 0 with:
```
mmcli -m 0
```

🔓 1. Unlock the SIM PIN
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

Now we need to create a bearer, a bearer in ModemManager is simply the data session that the modem uses to carry IP traffic. Think of it as the “pipe” that connects your modem to the mobile network for internet access.


🔌 2. If the bearer is active, disconnect it first
```
sudo mmcli -b 0 -d
```
❌ 3. Delete the bearer
Once disconnected, you can remove it:
```
sudo mmcli -m 0 --delete-bearer=0
``` 
Replace 0 with the bearer ID you saw earlier.

If successful, ModemManager will no longer list it.

2️⃣ Create a bearer (APN)
You must provide the APN for Auchan Telecom (France).
Auchan Telecom APN is typically:
```
APN: sl2sfr
```
(no username/password)

Create the bearer:
```
sudo mmcli -m 0 --create-bearer="apn=sl2sfr,ip-type=ipv4v6"
```

You should get something like:

> Successfully created bearer /org/freedesktop/ModemManager1/Bearer/0

3️⃣ Connect the bearer
```
sudo mmcli -b 0 --connect
```
Verify:
```
mmcli -b 0
```
You should see:
> status: connected
> or
> connected: yes


📶 2. Make sure the modem is enabled
Sometimes ModemManager leaves it disabled:
```
sudo mmcli -m 0 -e
```
return:
>successfully enabled the modem
Check if a bearer already exists:
```
mmcli -m 0
```
Look for a Bearer section (usally the last one):
>Bearer | paths: /org/freedesktop/ModemManager1/Bearer/0

If you see one, note its number and skip to Step 4.


3️⃣ check the exposed interfaces:

```
ls /sys/class/net
```
If you see:

* usb0 → ECM/RNDIS
* wwan0 → MBIM/QMI
* cdc-wdm0 → MBIM
* qmi_wwan → QMI


🚀 Bring the connection up with ModemManager
```
mmcli -m 0 --simple-connect="apn=your.apn"
```
Then check:
```
ip addr show usb0
```
If the modem assigns IP, you’ll see it.


3️⃣ Then check ttyUSB6 interface appears:
```
nmcli device status
```
Example output you might see:
>ttyUSB6        gsm       disconnected    --

✅ 4. Ask NetworkManager which interfaces it manages
```
nmcli -f GENERAL.STATE,GENERAL.DEVICE device show
```
in the list check ttyUSB6 as:
>30 (disconnected) → managed
>or
>100 (connected) → managed

Here ttyUSB6 is your SIMCOM SIM8230G modem control port.
👉 usb0 is NOT the data interface on your SIM8230G
👉 Your modem is exposing a GSM-style data port, not USB-ECM

That’s why:
👉 usb0 never gets an IP
👉 NetworkManager never manages it
👉 ttyUSB6 appears as gsm
👉 ModemManager connects but no interface shows up

This means your SIM8230G is currently in PPP (serial) mode, not ECM/MBIM.

Add a mobile broadband connection

Create a GSM/3G/4G connection using the modem:
* ifname "*" tells NM to pick the modem device automatically
* apn sl2sfr → your carrier’s APN
* ipv6.method ignore → optional, prevents IPv6 issues
```
sudo nmcli connection add type gsm ifname "*" con-name lte-gsm apn sl2sfr ipv4.method auto ipv6.method ignore
```

You should see:
>Connection 'lte-gsm' (315b84f6-9307-4bca-92d3-c25ec422f7b3) successfully added.

Bring the connection up:
```
sudo nmcli connection up lte-gsm
```

Check if PPP interface appears:
```
ip link
```
You should see ppp0 once connected.

1️⃣ Confirm NM sees usb0 at all
SIMCOM SIM8230G is operating in USB-ECM (Ethernet) mode, not as a classic wwan0 (QMI/MBIM) interface.
```
nmcli device status
```
You should see something like:
>usb0  ethernet  disconnected  --
>or 
>usb0  ethernet  unmanaged --
if it is unmanaged, force Network Manager to manage USB0
```
sudo nmcli device set usb0 managed yes
```
Re-check:
```
nmcli device status
```
3️⃣ Explicitly bind the connection to usb0
Edit the connection:
```
sudo nmcli connection modify lte-usb connection.interface-name usb0
```
Verify:
```
nmcli connection show lte-usb | grep interface-name
```
Should output:
>connection.interface-name: usb0

3️⃣ Create a connection profile for the modem (ECM)

Create a simple DHCP Ethernet profile:
```
sudo nmcli connection add \
  type ethernet \
  ifname usb0 \
  con-name lte-usb \
  ipv4.method auto \
  ipv6.method auto
```
4️⃣ Bring the connection up
```
sudo nmcli connection up lte-usb
```
If successful, you should immediately get an IPv4 address.

5️⃣ Verify IP, route, DNS
```
ip addr show usb0
ip route
resolvectl status
```

🌐 3. Configure APN (required for data)
```
sudo nmcli c add type gsm ifname "*" con-name simcom apn auchan
```
```
nmcli c up simcom
```

