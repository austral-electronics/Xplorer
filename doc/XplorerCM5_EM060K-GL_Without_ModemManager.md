# XPLORER CM5 - Configure the QUECTEL EM060K-GL 4G LTE-A modem without ModemManager

Check that you have a Linux version without network Manager.  
See the EM60K-GL specification in the hardware documentation

```
lsusb
```
```
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 001 Device 002: ID 2c7c:030b Quectel Wireless Solutions Co., Ltd. EM060K-GL
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 003 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 004 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 004 Device 002: ID 0403:6011 Future Technology Devices International, Ltd FT4232H Quad HS USB-UART/FIFO IC
Bus 005 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
```
```
ls /dev/ttyUSB*
```
```
/dev/ttyUSB0  /dev/ttyUSB2  /dev/ttyUSB4  /dev/ttyUSB6
/dev/ttyUSB1  /dev/ttyUSB3  /dev/ttyUSB5  /dev/ttyUSB7
```
ttyUSB0..3 correspond to the FT4232H (USB2 to 4 uart)
ttyUSB4..7 correspond to the EM060K-GL (LTE modem)
Connect with minicom (exit with 'Ctrl A' then 'q' then 'yes'):
```
sudo apt-get install minicom
```
```
sudo minicom -D /dev/ttyUSB6
```

#### Test LTE communication

In case of problems, Return to factory configuration and reset with :
```
AT+QPRTPARA=3
AT+CFUN=1,1

```

Enable echo sending the AT command and request SIM status in text :
```
ATE1
AT+CMEE=2
AT+CPIN?

```
- **Case : "SIM not inserted"**
If the response is :
```
OK
+CME ERROR: SIM not inserted

AT+QCCID
+CME ERROR: SIM failure
```
If the card is inserted and you have this error, It is likely a problem with the logical sense of the SIM card detection switch with the Quectel modules. Disable the SIM detect, restart the module and try again:
```
AT+QSIMDET=0,0
AT+CFUN=1,1

```
Or configure for a normaly Open SIM card connector and restart
```
AT+QSIMDET=1,0
AT+CFUN=1,1

```

- **Case :"SIM PIN"** : SIM PIN Required -> here PIN=0000
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

- **Case :"READY"** : The SIM is OK 

Test de SIM registration and status (check network connectivity without any data charge):
```
AT+CEREG?

```
Respond :
```
+CEREG: 2,4
OK
```
more : https://forums.quectel.com/t/how-to-test-sim-registration-and-status/3598/2

Send the following command RNDIS dialing in minicom:
```
AT+QENG="servingcell"
AT+QCFG="usbnet",1
AT+CFUN=1,1
```
you must see the response:
```
+QENG: "servingcell","SEARCH" 
OK                                             
OK                                         
```
After rebooting the module, the NET indicator is on, check the network status with the following command (optional):
```
AT+QENG="servingcell"
```
Using the following commands to get IP and set DNS:
```
sudo apt install isc-dhcp-client udhcpc
sudo dhclient -v usb0
sudo udhcpc -i usb0
sudo route add -net 0.0.0.0 usb0
```
After dialing, in the Xplorer CM5, you can see usb0 gets ip with the following commands:
```
$ ifconfig

usb0:  ...
```
Test usb0 and the network status:
```
ping -I usb0 www.google.com
```


#### Test GNSS
Enable the GNSS and get the positioning information with the AT commands:
```
AT+QGPS=1
AT+QGPSGNMEA="GGA"
```
Open another ssh console and view the GNSS NMEA0183 flow on ttyUSB5 with:
```
cat /dev/ttyUSB5
```
You can disable the GNSS with this AT command:
```
AT+QGPSEND
```

#### Basic Quectel AT Commands

| Command| Description| Return Value                                                                          
|----------------|-------------|-|
| AT | AT test command | OK
| ATE1 | Enables echo | OK
| ATE0 | Disables echo | OK
| ATI | Query brand, model anf firmware version | OK
| AT+CGMI | Query module manufacturers | OK
| AT+CGMM | Query module model | OK
| AT+CGSN | Query product serial numbers | OK
| AT+CSUB | Query module version and chip | OK
| AT+CGMR | Query firmware version serial numbers | OK
| AT+IPR? | Set the module hardware serial port baud rate | +IPR: OK
| AT+CPIN? | Query SIM card status, return READY, SIM card can be recognized normally | +CPIN: READY
| AT+COPS? | Query the current operator, the operator information will be returned after normal networking | +COPS: OK
| AT+CGREG? | Check network registration status | +CGREG: OK
| AT+QENG="servingcell" | Query UE system information | OK
| AT+QCFG="nwscanmode" | Network mode query: (0: Auto, 2 WCDMA only, 3 LTE Only...) | OK
| AT+CFUN=1,1 | Reset module | OK

- AT+QGMR: send command to query the detailed version of firmware;
- AT+CIMI: query the number of SIM card;
- AT+CPIN?: query the number of SIM card;
- AT+QGPS?: query the status of GPS but it's necessary to connect GPS antenna;
- AT+QGPSLOC?: query GPS location but it's necessary to connect GPS antenna;
- AT+CSQ: query signal value;
- AT+QGPS=1: send command to enable GPS because by default or powered off it's disabled;
- AT+QGPS=0: send command to disable GPS;
- AT+CFUN=1,1: send command to reboot the module;
- AT+QPRTPARA=3: send command to restore it to the default factory settings;
- AT+CGDCONT?: send command to read PDP context
- AT+CGDCONT=<cid>[,<PDP_type>[,<APN>[,<PDP_addr>[,<data_comp>[,<head_comp>]]]]]: send command to define PDP context with APN;
- AT+QPRTPARA=3: send command to restore to the default factory settings after upgrading.
- AT+CBC: query the voltage value

Links :
https://www.waveshare.com/wiki/EM060K-GL
https://www.waveshare.com/wiki/EM060K-GL_LTE_Cat-6_HAT
