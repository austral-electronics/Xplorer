# XPLORER CM5 - Configure the SIM8230G 5G RedCap Modem without ModemManager
  
Check that you have a Linux version without network Manager
```
uname -a
```
```
Linux xplorercm5 6.12.47+rpt-rpi-2712 #1 SMP PREEMPT Debian 1:6.12.47-1+rpt1 (2025-09-16) aarch64 GNU/Linux
```
Check the SIM8230G detection
```
lsusb
```
Wrong USB driver (1e0e:907b)
```
Bus 001 Device 002: ID 1e0e:907b Qualcomm / Option SDXBAAGHA-IDP _SN:ED48BEDF
```
Good USB driver (ID 1e0e:9078)
```
...
Bus 001 Device 002: ID 1e0e:9078 Qualcomm / Option SDXBAAGHA-IDP _SN:291E1C0C
....
```
```
lsusb -t
```
Wrong USB driver (rndis_host)
```
/:  Bus 001.Port 001: Dev 001, Class=root_hub, Driver=dwc2/1p, 480M
    |__ Port 001: Dev 002, If 0, Class=Miscellaneous Device, Driver=rndis_host, 480M
    |__ Port 001: Dev 002, If 1, Class=CDC Data, Driver=rndis_host, 480M
    |__ Port 001: Dev 002, If 2, Class=Vendor Specific Class, Driver=option, 480M
    |__ Port 001: Dev 002, If 3, Class=Vendor Specific Class, Driver=option, 480M
    |__ Port 001: Dev 002, If 4, Class=Vendor Specific Class, Driver=option, 480M
...
```

Good USB Driver (cdc_ether)

```
/:  Bus 001.Port 001: Dev 001, Class=root_hub, Driver=dwc2/1p, 480M
    |__ Port 001: Dev 002, If 0, Class=Vendor Specific Class, Driver=option, 480M
    |__ Port 001: Dev 002, If 1, Class=Vendor Specific Class, Driver=option, 480M
    |__ Port 001: Dev 002, If 2, Class=Vendor Specific Class, Driver=option, 480M
    |__ Port 001: Dev 002, If 3, Class=Communications, Driver=cdc_ether, 480M
    |__ Port 001: Dev 002, If 4, Class=CDC Data, Driver=cdc_ether, 480M
...
```
```
ls /dev/ttyUSB*
```
```
/dev/ttyUSB0  /dev/ttyUSB1  /dev/ttyUSB2  /dev/ttyUSB3
```

With bookworm and depending of the module software version, you have not ttyUSB4 to ttyUSB6 you must load dynamically the driver descriptor with the following commands :
```
sudo modprobe option
sudo sh -c 'echo "1e0e 9073" > /sys/bus/usb-serial/drivers/option1/new_id'
sudo sh -c 'echo "1e0e 9071" > /sys/bus/usb-serial/drivers/option1/new_id'
sudo sh -c 'echo "1e0e 9072" > /sys/bus/usb-serial/drivers/option1/new_id'
sudo sh -c 'echo "1e0e 9078" > /sys/bus/usb-serial/drivers/option1/new_id'
sudo sh -c 'echo "1e0e 907b" > /sys/bus/usb-serial/drivers/option1/new_id'
```

You must see 3 new descriptor :
```
ls /dev/ttyUSB*
```
Response:
```
/dev/ttyUSB0  /dev/ttyUSB1  /dev/ttyUSB2  /dev/ttyUSB3  /dev/ttyUSB4  /dev/ttyUSB5  /dev/ttyUSB6
```

Install and open minicom :
```
sudo apt-get install minicom
```
```
sudo minicom -D /dev/ttyUSB6
```
You must focre the PID/VID USB of the modem to a Linux compatible MBIM/QMI profile. Send the following command via minicom :
```
at+cusbcfg=usbid,1e0e,9078
```
Wait one minute 🥐☕ for the module to restart until the SIM status display:
```
....
+CPIN: SIM PIN
OK
SIMCOM_SIM8230G
OK
OK
```

Open another terminal, After dialing, you can see that **usb0** gets or not the IP address through the following command:
```
ifconfig
```
Display usb0 without inet address:
```
usb0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet6 fe80::e3d6:7553:3c79:279b  prefixlen 64  scopeid 0x20<link>
        ether 0e:57:8e:fe:89:0d  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
        
...
```
With minicom send Mode echo, Turn off the fly mode, show SIM Status:

```
ATE1
AT+CMEE=2
AT+CPIN?

```
Response :
```
+CPIN: SIM PIN
OK
```
If needed enter the SIM PIN (Replace 0000 with your PIN):
```
AT+CPIN="0000"

```
Response :
```
OK
+CPIN: READY
SMS DONE
PB DONE
```
Wait 30 seconds to 1 minute to get the operator :
```
AT+COPS?

```
```
+COPS: 0,0,"AUCHAN TELECOM",7   <-- Here your Mobile operator 
OK
```
If still no operator, try to turn off the flight mode, set the network to auto-seek, and verify the signal level and retry ```AT+COPS?```:
```
AT+CFUN=1

```
```
AT+CNMP=2

```
```
AT+CSQ

```
Response:
```
+CSQ: 23,99
OK
```
note : 15–31 → good signal, 10–14 → mid, <10 → bad, 99 → no signal

Verify LTE/5G :
```
AT+QENG="servingcell"

```
Response:
```
+QENG:"servingcell","CONNECT","LTE","FDD",208,20,130336514,56,EUTRAN-BAND3,1850,5,5,0x7848,-1166,-167,-796,0,8,-99,9
OK
```
Test if data valid (1=Yes) :
```
AT+CGATT?

```
Response:
```
+CGATT: 1
OK
```
Check internet connection :
```
AT+CPSI?

```
Response
```
AT+CPSI?
+CPSI: LTE,Online,208-10,0x7848,130336523,154,EUTRAN-BAND3,1501,5,5,-167,-1172,-810,-4
```
Test APN profil  
```
AT+CGDCONT?

```
Response:
```
+CGDCONT: 1,"IPV6","mmsbouygtel.com","0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0",0,0,0,0,,,,,,,,,,"",,,,0
+CGDCONT: 2,"IPV4V6","ims","0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0",0,0,0,0,,,,,,,,,,"",,,,0
+CGDCONT: 3,"IPV4V6","sos","0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0",0,0,0,1,,,,,,,,,,"",,,,0
OK
```
The CID 1 gives the active APN name is in our case **mmsbouygtel.com**, you will need this name to configure Network Manager.

Check for the IP V4 address:
```
ifconfig
```
```
...
usb0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.225.209  netmask 255.255.255.0  broadcast 192.168.225.255
        inet6 fe80::e3d6:7553:3c79:279b  prefixlen 64  scopeid 0x20<link>
        ether de:10:d1:3a:30:42  txqueuelen 1000  (Ethernet)
        RX packets 59  bytes 5769 (5.6 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 67  bytes 9802 (9.5 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
...
```
Show network manager status
```
clear && nmcli connection show && nmcli device status && ip a
```
```
NAME        UUID                                  TYPE      DEVICE 
wired_eth0  b58c1394-1af4-4241-9ae7-5dd284df1b06  ethernet  eth0   
wired_usb0  257ae364-2f98-4712-b297-d7a61ec85cf3  ethernet  usb0   
lo          2d4f2dd8-e60f-4111-8d18-b613287b253d  loopback  lo     
DEVICE         TYPE      STATE                   CONNECTION 
eth0           ethernet  connected               wired_eth0 
usb0           ethernet  connected               wired_usb0 
lo             loopback  connected (externally)  lo         
wlan0          wifi      disconnected            --         
p2p-dev-wlan0  wifi-p2p  disconnected            --         
can0           can       unmanaged               --         
can1           can       unmanaged               --         
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 88:a2:9e:30:a5:6a brd ff:ff:ff:ff:ff:ff
    inet 10.10.10.139/24 brd 10.10.10.255 scope global dynamic noprefixroute eth0
       valid_lft 41520sec preferred_lft 41520sec
    inet6 fe80::773e:6bf6:3e40:92ce/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
3: can0: <NOARP,UP,LOWER_UP,ECHO> mtu 16 qdisc pfifo_fast state UP group default qlen 10
    link/can 
4: can1: <NOARP,ECHO> mtu 16 qdisc noop state DOWN group default qlen 10
    link/can 
5: wlan0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc fq_codel state DOWN group default qlen 1000
    link/ether 88:a2:9e:30:a5:6b brd ff:ff:ff:ff:ff:ff
7: usb0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UNKNOWN group default qlen 1000
    link/ether 0e:57:8e:fe:89:0d brd ff:ff:ff:ff:ff:ff
    inet 192.168.225.209/24 brd 192.168.225.255 scope global dynamic noprefixroute usb0
       valid_lft 42433sec preferred_lft 42433sec
    inet6 2a04:cec0:1162:f6de::206/128 scope global dynamic noprefixroute 
       valid_lft 42487sec preferred_lft 28087sec
    inet6 2a04:cec0:1162:f6de:5e:69d8:59e5:b95c/64 scope global dynamic noprefixroute 
       valid_lft 43018sec preferred_lft 28618sec
    inet6 fe80::e3d6:7553:3c79:279b/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
```
## No usb0 IP V4 Address issue
You may have an incorrect APN (MMS and not Data):

**Solution 1 :**
Send the AT command, Replace the name with your APN name:
```
AT+CGDCONT=1,"IPV4V6","mmsbouygtel.com"
```
Verify IP V4 Address in another terminal:
```
ip link
```

```
sudo apt-get install isc-dhcp-client
sudo dhclient usb0
```
Verify :
```
ip a
```
```
...
7: usb0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UNKNOWN group default qlen 1000
    link/ether 3a:77:44:07:54:5d brd ff:ff:ff:ff:ff:ff
    inet 192.168.225.212/24 brd 192.168.225.255 scope global dynamic usb0
       valid_lft 42218sec preferred_lft 42218sec
```
```
ip route
```
```
default via 192.168.225.1 dev usb0 
default via 10.10.10.1 dev eth0 proto dhcp src 10.10.10.235 metric 100 
10.10.10.0/24 dev eth0 proto kernel scope link src 10.10.10.235 metric 100 
192.168.225.0/24 dev usb0 proto kernel scope link src 192.168.225.212 
```

**Solution 2 : (Not Tested)**
```
AT+NETOPEN
```
```
OK
```
```
AT+NETOPEN?
AT+IPADDR
AT+CGPADDR=1
```


**Or have a dhcp configuration to do:**
If unable to obtain an usb0 IP Address or successfully connect to the Internet:
```
sudo apt-get install udhcpc isc-dhcp-client
sudo dhclient -v usb0
sudo udhcpc -i usb0
sudo route add -net 0.0.0.0 usb0
```
## Test the cellular connection
**Test 1:  ping google without DNS :**
```
ping -c3 -I usb0 8.8.8.8
```
```
PING 8.8.8.8 (8.8.8.8) from 192.168.225.209 usb0: 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=110 time=138 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=110 time=48.2 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=110 time=37.6 ms

--- 8.8.8.8 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2002ms
rtt min/avg/max/mdev = 37.638/74.463/137.544/44.812 ms
...
```
**Test 2 : ping google with DNS :**
```
ping -c3 -I usb0 google.com
```
```
PING google.com (2a00:1450:4007:818::200e) from 2a04:cec0:10d7:8595::206 usb0: 56 data bytes
64 bytes from par21s20-in-x0e.1e100.net (2a00:1450:4007:818::200e): icmp_seq=1 ttl=114 time=40.9 ms
64 bytes from par21s20-in-x0e.1e100.net (2a00:1450:4007:818::200e): icmp_seq=2 ttl=114 time=57.9 ms
64 bytes from par21s20-in-x0e.1e100.net (2a00:1450:4007:818::200e): icmp_seq=3 ttl=114 time=46.2 ms

--- google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2004ms
rtt min/avg/max/mdev = 40.940/48.338/57.894/7.087 ms
```
**Test 3: Download and show a test file :**
```
curl --interface usb0 -sL https://raw.github.com/austral-electronics/Xplorer/main/README.md
```

## DNS Server issue

Sometimes you can ping an IP but not a domain name, which is a DNS server issue. Please refer to the following steps to configure the DNS server Check the current DNS
```
cat /etc/resolv.conf
```
Backup the original DNS configuration file first
```
sudo mv /etc/resolv.conf resolv_bk.conf
```
Add a universal DNS server
```
domain lan
nameserver 192.168.225.1
nameserver 8.8.8.8.    <-- add this line
```
Go ping the domain name for testing :
```
ping google.com -I usb0
ping 8.8.8.8 -I usb0
```
Lock the file to prevent tampering, unlock and change to - i
```
sudo chattr +i /etc/resolv.conf
```
## Disable/Enable the cellular connection
You can disable the network interfaces exposed by the cellular module:
```
sudo ip link set dev usb0 down
```
And enable it with :
```
sudo ip link set dev usb0 up
```

## No Ethernet ssh console
```
nmcli connection show
```
```
NAME                          UUID                                  TYPE      DEVICE 
netplan-eth0                  75a1216a-9d1a-30cd-8aca-ace5526ec021  ethernet  eth0   
lo                            316df1f3-0080-4b19-b29a-2d269f7b0794  loopback  lo     
netplan-wlan0-creafab_invite  6ca05510-730d-3114-9fde-0ed21ad066ab  wifi      --     
```

```
sudo nmcli connection modify "netplan-eth0" \
  ipv4.method auto \
  ipv6.method ignore \
  ipv4.route-metric 100 \
  connection.autoconnect yes
```
```
nmcli device disconnect eth0
nmcli device connect eth0
```
```
ip a show eth0
```

```
sudo nmcli connection modify "usb0" \
  ipv4.never-default yes \
  ipv6.never-default yes \
  ipv4.route-metric 300 \
  ipv6.route-metric 300
```
```
nmcli connection down "usb0"
nmcli connection up "usb0"
```
```
ip a show eth0
```
```
ip route
```
eth0 in priority

Force eth0 priority:
```
sudo nmcli connection modify "netplan-eth0" ipv4.route-metric 100
sudo nmcli connection modify "netplan-eth0" ipv6.route-metric 100
```
No eth0 desactivation:
```
sudo nmcli connection modify "netplan-eth0" connection.autoconnect yes
sudo nmcli connection modify "netplan-eth0" connection.autoconnect-priority 10
```
Low usb0 priority:
```
sudo nmcli connection modify "usb0" ipv4.route-metric 300
sudo nmcli connection modify "usb0" ipv6.route-metric 300
sudo nmcli connection modify "usb0" connection.autoconnect-priority -10
```
```
sudo systemctl restart NetworkManager
```


## Using Trixie or NetworkManager
For old Debian before Trixie, install and restart ModemManager and NetworkManager
```
sudo apt install -y network-manager modemmanager libqmi-utils libmbim-utils
```
```
sudo systemctl restart ModemManager NetworkManager
```
Nota that after restart you must wait a minute until this AT status :
```
+CPCMREG: (0-1)                                                                 
OK
```
See Logs:
```
journalctl -u NetworkManager
```
```
journalctl -u ModemManager 
```

Verify the Modem detection :
```
mmcli -L
```
```
    /org/freedesktop/ModemManager1/Modem/0 [SIMCOM INCORPORATED] SIMCOM_SIM8230G
```
Verify the SIM PIN status :
```
mmcli -m 0
```
Unlock SIM PIN
```
mmcli -i 0
```
Send sim pin
```
sudo mmcli -i 0 --pin=0000
```
## Automate VID/PID Rule
lsub before correction :

lsub after correction :
```
Bus 001 Device 003: ID 1e0e:9078 Qualcomm / Option SDXBAAGHA-IDP _SN:291E1C0C
```
Create a rule
```
sudo nano /etc/udev/rules.d/99-sim8230-usbid.rules
```
With
```
ACTION=="add", SUBSYSTEM=="usb", ATTR{idVendor}=="1e0e", \
  RUN+="/usr/bin/mmcli -m 0 --command=AT+CUSBCFG=USBID,1E0E,9078"
  RUN+="/usr/bin/mmcli -m 0 --reset"
```
Reload
```
sudo udevadm control --reload
sudo reboot
```
## Configure SIM PIN unsing networkManager
```
sudo nmcli connection modify auchan-5g gsm.pin 0000
```
```
nmcli connection show auchan-5g | grep gsm.pin
```
```
sudo chmod 600 /etc/NetworkManager/system-connections/auchan-5g.nmconnection
```
```
sudo reboot
```




For cellular connections, first install the modem-manager snap with:
https://snapcraft.io/install/modem-manager/raspbian

https://documentation.ubuntu.com/core/explanation/system-snaps/network-manager/how-to-guides/configure-cellular-connections/

https://forums.raspberrypi.com/viewtopic.php?t=283603

https://techship.com/support/faq/how-to-step-by-step-set-up-a-data-connection-over-qmi-interface-using-qmicli-and-in-kernel-driver-qmi-wwan-in-linux/

techship.com/support/faq/how-to-step-by-step-set-up-a-data-connection-over-qmi-interface-using-qmicli-and-in-kernel-driver-qmi-wwan-in-linux/

```
sudo apt update
sudo apt install snapd
sudo reboot
sudo snap install snapd
sudo snap install modem-manager

```
Check whether a modem was properly detected via:
```
$ sudo modem-manager.mmcli -L
Found 1 modems:
    /org/freedesktop/ModemManager1/Modem/0 [description]
```


# 5G RED-CAP (3GPP 5G Release 17)
Compatible with Direct To Cell

https://www.waveshare.com/sim8230g-m2.htm
https://www.waveshare.com/wiki/SIM8230G-M2
https://techship.com/support/faq/how-to-automatically-set-up-and-maintain-the-cellular-data-connection-in-headless-raspberry-pi-os-raspbian-systems/

### SIM8230 troubleshoot
https://techship.com/product/simcom-sim8230g-m2-5g-redcap-m2/?variant=003&tab=faq&page=1

```
uname -a
```
```
Linux xplorercm5 6.12.47+rpt-rpi-2712 #1 SMP PREEMPT Debian 1:6.12.47-1+rpt1 (2025-09-16) aarch64 GNU/Linux
```
```
ls -l /dev/serial/by-id
```
```
...
lrwxrwxrwx 1 root root 13 Jan  9 14:25 usb-SIMCOM_SDXBAAGHA-IDP__SN:291E1C0C_0123456789ABCDEF-if00-port0 -> ../../ttyUSB4
lrwxrwxrwx 1 root root 13 Jan  9 14:25 usb-SIMCOM_SDXBAAGHA-IDP__SN:291E1C0C_0123456789ABCDEF-if01-port0 -> ../../ttyUSB5
lrwxrwxrwx 1 root root 13 Jan  9 14:25 usb-SIMCOM_SDXBAAGHA-IDP__SN:291E1C0C_0123456789ABCDEF-if02-port0 -> ../../ttyUSB6
```
```
ls -l /sys/bus/usb-serial/devices
```
```
...
lrwxrwxrwx 1 root root 0 Jan  9 14:49 ttyUSB4 -> ../../../devices/platform/axi/1000480000.usb/usb1/1-1/1-1:1.0/ttyUSB4
lrwxrwxrwx 1 root root 0 Jan  9 14:49 ttyUSB5 -> ../../../devices/platform/axi/1000480000.usb/usb1/1-1/1-1:1.1/ttyUSB5
lrwxrwxrwx 1 root root 0 Jan  9 14:49 ttyUSB6 -> ../../../devices/platform/axi/1000480000.usb/usb1/1-1/1-1:1.2/ttyUSB6
```
```
dmesg
```
```
...
[   12.113642] usb 1-1: new high-speed USB device number 2 using dwc2
[   12.306362] usb 1-1: New USB device found, idVendor=1e0e, idProduct=9078, bcdDevice= 5.15
[   12.306370] usb 1-1: New USB device strings: Mfr=1, Product=2, SerialNumber=3
[   12.306373] usb 1-1: Product: SDXBAAGHA-IDP _SN:ED48BEDF
[   12.306375] usb 1-1: Manufacturer: SIMCOM
[   12.306376] usb 1-1: SerialNumber: 0123456789ABCDEF
[   12.340966] cdc_ether 1-1:1.3 usb0: register 'cdc_ether' at usb-1000480000.usb-1, CDC Ethernet Device, 42:10:41:a1:53:15
[   12.341017] usbcore: registered new interface driver cdc_ether
[  114.200285] usbcore: registered new interface driver option
[  114.200312] usbserial: USB Serial support registered for GSM modem (1-port)
[  114.250122] option 1-1:1.0: GSM modem (1-port) converter detected
[  114.250250] usb 1-1: GSM modem (1-port) converter now attached to ttyUSB4
[  114.250330] option 1-1:1.1: GSM modem (1-port) converter detected
[  114.250417] usb 1-1: GSM modem (1-port) converter now attached to ttyUSB5
[  114.251202] option 1-1:1.2: GSM modem (1-port) converter detected
[  114.251361] usb 1-1: GSM modem (1-port) converter now attached to ttyUSB6
[  184.720826] dwc2 1000480000.usb: Not connected
[  184.720882] dwc2 1000480000.usb: Not connected
[  184.720886] dwc2 1000480000.usb: Not connected
[  184.720894] dwc2 1000480000.usb: Not connected
[  184.720947] dwc2 1000480000.usb: Not connected
[  184.720960] dwc2 1000480000.usb: Not connected
[  184.720964] dwc2 1000480000.usb: Not connected
[  184.914551] usb 1-1: USB disconnect, device number 2
[  184.914743] option1 ttyUSB4: GSM modem (1-port) converter now disconnected from ttyUSB4
[  184.914765] option 1-1:1.0: device disconnected
[  184.915047] option1 ttyUSB5: GSM modem (1-port) converter now disconnected from ttyUSB5
[  184.915071] option 1-1:1.1: device disconnected
[  184.915224] option1 ttyUSB6: GSM modem (1-port) converter now disconnected from ttyUSB6
[  184.915238] option 1-1:1.2: device disconnected
[  184.915286] cdc_ether 1-1:1.3 usb0: unregister 'cdc_ether' usb-1000480000.usb-1, CDC Ethernet Device
[  204.662801] usb 1-1: new high-speed USB device number 3 using dwc2
[  204.855506] usb 1-1: New USB device found, idVendor=1e0e, idProduct=9078, bcdDevice= 5.15
[  204.855513] usb 1-1: New USB device strings: Mfr=1, Product=2, SerialNumber=3
[  204.855516] usb 1-1: Product: SDXBAAGHA-IDP _SN:ED48BEDF
[  204.855519] usb 1-1: Manufacturer: SIMCOM
[  204.855522] usb 1-1: SerialNumber: 0123456789ABCDEF
[  204.859240] option 1-1:1.0: GSM modem (1-port) converter detected
[  204.859372] usb 1-1: GSM modem (1-port) converter now attached to ttyUSB4
[  204.859503] option 1-1:1.1: GSM modem (1-port) converter detected
[  204.859575] usb 1-1: GSM modem (1-port) converter now attached to ttyUSB5
[  204.859839] option 1-1:1.2: GSM modem (1-port) converter detected
[  204.859911] usb 1-1: GSM modem (1-port) converter now attached to ttyUSB6
[  204.876234] cdc_ether 1-1:1.3 usb0: register 'cdc_ether' at usb-1000480000.usb-1, CDC Ethernet Device, 4a:ac:a7:54:f8:49
...
```

Test AT command :
```
AT 
ATE1 
ATI 
AT&V 
AT+SIMCOMATI 
AT+CMEE=2 
AT+CEER 
AT+CGMR 
AT+CSUB 
AT+CGSN 
AT+CUSBCFG? 
AT+CUSBPIDSWITCH? 
AT+CPCIEMODE? 
AT+UIMHOTSWAPON? 
AT+UIMHOTSWAPLEVEL? 
AT+SMSIMCFG? 
AT+CFUN? 
AT+CPIN? 
AT+CPSI? 
AT+CNSMOD? 
AT+CNWINFO? 
AT+CNMP? 
AT+CNBP? 
AT+CNAOP? 
AT+CSYSSEL=? 
AT+CSYSSEL="lte_band" 
AT+CSYSSEL="w_band" 
AT+CSYSSEL="rat_acq_order" 
AT+COPS? 
AT+CREG=2 
AT+CREG? 
AT+CGREG=2 
AT+CGREG? 
AT+CEREG=2 
AT+CEREG? 
AT+CSQ 
AT+CGATT? 
AT+CGDCONT? 
AT$QCPDPP? 
AT+CGAUTH? 
AT+CGACT? 
AT+CGPADDR 
AT+CGCONTRDP 
AT$QCRMCALL? 
AT+CPMUTEMP 
AT+CCPUTEMP=2 
AT+CBC

```
For a working cellular connection with a 4G LTE SIM:
```
OK
AT 
OK
ATI 
Manufacturer: SIMCOM INCORPORATED
Model: SIMCOM_SIM8230G
Revision: V1.0.00
IMEI: 860488070026329
+GCAP: +CGSM

OK
AT+SIMCOMATI
Manufacturer: SIMCOM INCORPORATED
Model: SIMCOM_SIM8230G
Revision: 2310B04X35M22A-M2
IMEI: 860488070026329

OK
AT$QCPDPP? 
$QCPDPP: 1,0
$QCPDPP: 2,0
$QCPDPP: 3,0

OK
AT 
OK
ATI 
Manufacturer: SIMCOM INCORPORATED
Model: SIMCOM_SIM8230G
Revision: V1.0.00
IMEI: 860488070026329
+GCAP: +CGSM

OK
AT+SIMCOMATI 
Manufacturer: SIMCOM INCORPORATED
Model: SIMCOM_SIM8230G
Revision: 2310B04X35M22A-M2
IMEI: 860488070026329

OK
AT+CEER 
+CEER: No cause information available

OK
AT+CSUB 
+CSUB: B04V02
+CSUB: SDX35_LE10_M2_M22_V1.07_250610

OK
AT+CUSBCFG? 
USBADB: 0
USBID: 0X1E0E,0X9078

OK
AT+CPCIEMODE? 
ERROR
AT+UIMHOTSWAPLEVEL? 
+UIMHOTSWAPLEVEL: 1,1
+UIMHOTSWAPLEVEL: 1,2

OK
AT+SMSIMCFG? 
+SMSIMCFG: 1,1,1
+SMSIMCFG: 1,2,0

OK
AT+CPIN? 
+CPIN: READY

OK
AT+CNSMOD? 
+CNSMOD: 0,8

OK
AT+CNWINFO? 
+CNWINFO: LTE,20820130336514,0x7C4C7,0,0,UNKOWN,UNKOWN,0,0,-99

OK
AT+CNBP? 
+CNBP: 0x0000000000000000,0x0000000000000042000087E22B0F38DF,0x00000000000000000

OK
AT+CSYSSEL=? 
+CSYSSEL: "nr5g_disable",(0-2)
+CSYSSEL: "nr5g_band",1:2:3:5:7:8:12:13:14:18:20:25:26:28:30:38:40:41:48:66:70:8
+CSYSSEL: "lte_band",1:2:3:4:5:7:8:12:13:14:17:18:19:20:25:26:28:30:34:38:39:401
+CSYSSEL: "rat_acq_order",9:12

OK
AT+CSYSSEL="w_band" 
ERROR
at_acq_order" 
ERROR
AT+CREG=2 
OK
AT+CGREG=2 
OK
AT+CEREG=2 
OK
AT+CSQ 
+CSQ: 19,99

OK
ATT? 
ERROR
AT$QCPDPP? 
$QCPDPP: 1,0
$QCPDPP: 2,0
$QCPDPP: 3,0

OK
AT+CGACT? 
+CGACT: 1,1
+CGACT: 2,0
+CGACT: 3,0

OK
AT+CGCONTRDP 
+CGCONTRDP: 1,5,"mmsbouygtel.com",42.4.206.192.17.98.246.222.0.0.0.93.102.159.11

OK
AT+CPMUTEMP 
+CPMUTEMP: 45

OK

```

And :
```
AT+CSYSSEL="nr5g_disable" 
AT+CSYSSEL="nr5g_band" 
AT+CSYSSEL="nsa_nr5g_band" 
AT+C5GREG=2 
AT+C5GREG? 
```
Gives :
```
AT+CSYSSEL="nr5g_disable" 
+CSYSSEL: "nr5g_disable",0

OK
AT+CSYSSEL="nsa_nr5g_band" 
+CSYSSEL: "nsa_nr5g_band",

OK
AT+C5GREG? 
+C5GREG: 0,0

OK
```

Usefull links :
https://www.waveshare.com/wiki/SIM8230G-M2
https://www.waveshare.com/wiki/SIM820X_RNDIS_Dial-Up
https://www.waveshare.com/wiki/GSM/GPRS/GNSS_HAT
https://forums.raspberrypi.com/viewtopic.php?t=345000

https://www.freedesktop.org/software/libqmi/man/latest/qmicli.1.html?__goaway_challenge=meta-refresh&__goaway_id=ca37fabede633bffe8a78366cb521465&__goaway_referer=https%3A%2F%2Fwww.google.com%2F

https://techship.com/product/simcom-sim8230g-m2-5g-redcap-m2/?variant=003&tab=faq&page=1

https://techship.com/support/faq/how-to-guide-automated-always-on-connection-with-simcom-sim8202x-m2-series-in-linux-using-the-rndis-usb-mode/
