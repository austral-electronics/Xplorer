# <code style="color : BLACK">XPLORER CM5 - Software Guide - 🅰🆄🆂🆃🆁🅰🅻 Electronics</code>
**Xplorer CM5 – Waterproof Rugged Industrial Edge IoT/AIoT Controller & Embedded Mission Computer – Raspberry PI CM5 & Hailo AI Ecosystems**  

Xplorer CM5 are a familly of products. They can be used when reliability is not an option for IIoT, AIoT & Edge Gateways or Controllers for Smart, Connected Automation and Supervision but also as Embedded Mission Computers for Sea, Air & Land Intelligent Mobility in harsh environment.

![image](https://github.com/austral-electronics/Xplorer/raw/main/images/Xplorer_CM5_Flex_Overview.png)
*[www.austral-eng.com](http://austral-eng.com/en/accueil-english-2/) - Intelligent Technologies for Marine, Industrial IoT and Unmanned Vehicles*  

---
# 📚 TABLE OF CONTENTS
- **[1 - INTRODUCTION](#1)**
- **[2 - FLASH AN IMAGE](#2)**
  - [2.1 Install the flashing tools on your computer](#2.1)
    - [2.1.1 Use RPIBOOT on Mac](#2.1.1)
  - [2.2 Flash procedure](#2.2)
- **[3 - GETTING STARTED](#3)**
    - [3.1 - Launch a SSH console](#3.1)
    - [3.2 - Update the linux and eeprom](#3.2)
    - [3.3 - Patch the configuration file](#3.3)
    - [3.4 - Enable I2C](#3.4)
    - [3.5 - Option : Activate a RS232 console](#3.5)
    - [3.6 - Option : Static IP configuration](#3.6)
    - [3.7 - Change Password](#3.7)
    - [3.8 - Installation of usefull tools](#3.8)
- **[4 - TEST THE PERIPHERALS](#4)**
    - [4.1 - Linux configuration](#4.1)
    - [4.2 - Ethernet](#4.2)
        - [4.2.1 - GbE over M12](#4.2.1)
        - [4.2.2 - 5 GbE over USB-C](#4.2.1)
    - [4.3 - WiFi/BT](#4.3)
    - [4.4 - Serials](#4.4)
        - [4.4.1 - UART0](#4.4.1)
        - [4.4.2 - COM1](#4.4.2)
        - [4.4.3 - COM2](#4.4.3)
        - [4.4.4 - COM3 in RS232 Mode](#4.4.4)
        - [4.4.5 - COM3 in RS485 Mode](#4.4.5)
        - [4.4.6 - COM4](#4.4.6)
        - [4.4.7 - RXDA](#4.4.7)
        - [4.4.8 - RXDB](#4.4.8)
        - [4.4.9 - RXDC](#4.4.9)
        - [4.4.10 - RXDD](#4.4.10)
    - [4.5 - CAN-FD](#4.5)
        - [4.5.1 - SPI](#4.5.1)
        - [4.5.2 - CAN1](#4.5.2)
        - [4.5.3 - CAN2](#4.5.3)
    - [4.6 - CyberSecurity](#4.6)
        - [4.6.1 - I2C](#4.6.1)
        - [4.6.2 - TPM2.0 Chip](#4.6.2)
        - [4.6.3 - CrytoAuthentication Co-Processor](#4.6.3)
    - [4.7 - Storages](#4.7)
        - [4.7.1 - PCIe peripherals](#4.7.1)
        - [4.7.2 - USB peripherals](#4.7.2)
        - [4.7.3 - Drives](#4.7.3)
        - [4.7.4 - Type-C External Flash Drive](#4.7.4)
        - [4.7.5 - Internal NVMe SSD(s)](#4.7.5)
        - [4.7.6 - Micro SD Card](#4.7.6)
    - [4.8 - DAQ](#4.8)
    - [4.9 - Cellular and Direct-To-Cell](#4.9)
        - [4.9.1 - Nano SIM](#4.9.1)
        - [4.9.2 - 4FF eSIM](#4.9.2)
        - [4.9.3 - 4G LTE-A](#4.9.3)
        - [4.9.4 - 5G RedCap](#4.9.4)
        - [4.9.5 - Speed Test](#4.9.5)
    - [4.10 - Multi-Protocol Wireless Network co-processor](#4.10)
        - [4.10.1 - Software development](#4.10.1)
        - [4.10.2 - Pre-build Firmware](#4.10.2)
        - [4.10.3 - UART Xmodem Bootload](#4.10.3)
            - [4.10.3.1 - Define the bootloader activation pin](#4.10.3.1)
            - [4.10.3.2 - Command NRST and NBOOT](#4.10.3.2)
            - [4.10.3.3 - Flash manually using Minicom](#4.10.3.3)
            - [4.10.3.4 - Firmware update with the NabuCasa Universal Silicon Labs Flasher](#4.10.3.4)
            - [4.10.3.5 - Firmware update with Silicon Labs Commander](#4.10.3.5)
        - [4.10.4 - Usefull Links](#4.10.4)
    - [4.11 - LoRa/Sigfox](#4.11)
    - [4.12 - RTC](#4.12)
- **[5 - TIPS](#5)**
    - [5.1 - Benchmark](#5.1)
    - [5.2 - Shrink a pi image](#5.2)
    - [5.3 - Manage Energy](#5.3)
    - [5.4 - Watchdog](#5.4)
    - [5.5 - NAS Setup](#5.5)
    - [5.6 - Reduce boot time](#5.6)
    - [5.7 - CPU Isolation and Task Affinity for Multicore Optimization](#5.7)
    - [5.8 - Security Hardening](#5.8)
- **[6 - GPIO CONFIGURATION](#6)**
- **[7 - SELF-TEST](#7)**
---
# 1 - INTRODUCTION <a name="1"></a>
Welcome to the **software guide for the Xplorer CM5**, a ruggedized industrial edge IoT / AIoT controller and mission computer designed for harsh environments based on the [Raspberry Pi CM5](https://www.raspberrypi.com/products/compute-module-5/?variant=cm5-104032) 🍓🥧 module. The Xplorer CM5 series is engineered for reliability where failure is not an option—ideal for smart automation, connected infrastructure, unmanned systems, and embedded intelligence projects.

In this guide, we will cover only software aspects of the Xplorer CM5:
 
- 🏁 Getting started: installing tools, flashing firmware, booting up, and basic setup  
- 🔧 Configuration and connectivity testing : Networks, Serials, CANbus, DAQ, Expansion M.2 modules (SSD, AI accelerator, Cellular, GNSS), optional welded modules (LoRa, Zigbee, Matter over Thread)    
- 🔋 Energy consumption optimization 
- 🧪 Supported operating systems and frameworks.

Where to find more documentation :

- For an overview on highlight and areas of application, please refer to our [Xplorer CM5 Web Page](https://austral-eng.com/en/xplorer-cm5/) or the [Xplorer CM5 Family Flyer](https://github.com/austral-electronics/Xplorer/tree/main/doc/Xplorer_CM5_OEM_Flyer.pdf).  
- Regarding essential specifications, verify integration, building your configuration, pricing and ordering, please refer to our [Xplorer CM5 Flex Brief Sheet](https://github.com/austral-electronics/Xplorer/tree/main/doc/Xplorer_CM5_Flex_Datasheet_01.pdf).
- Regarding detailed specifications, options, hardware architecture, electrical wiring and installation, maintenance, Please refer to the [Xplorer CM5 Flex Web Datasheet](https://github.com/austral-electronics/Xplorer/tree/main/doc/XplorerCM5_Flex_Datasheet.md).
- When it comes to online software support for the features of this product, you've come to the right place, but you'll also may need to consult the extensive [documentation provided by the Raspberry Pi Foundation](https://www.raspberrypi.com/documentation/) and if you're working with AI, check out [Hailo's resources](https://hailo.ai/resources/).

How to get support :

- One of the greatest strengths of this ecosystem is the **reliability of the OS** with its **periodic updates** that help you keep up if you want with the last software developments and its vibrant community that can help you solve problems that are difficult to overcome and ensure that your company does not need multiple specialists. Consider joining the [official Raspberry Pi forums](https://forums.raspberrypi.com/).
- Check [YouTube](https://www.youtube.com/results?search_query=raspberry+pi) regularly to keep up to date with the latest news and find countless tutorials.
- [Austral Electronics](https://austral-eng.com/en/electronics-and-embedded-computing/) is a design office, we can support you on your specific needs in electronics, embedded computing, marine protocols, specific Linux, sector specific certification... Contact our customer support at contact@austral-eng.com.

Whether you're integrating Xplorer CM5 into industrial systems, vehicle, marine or unmanned platforms, or deploying AI at the edge, this tutorial walks you step-by-step through the essential software setup and usage. Let’s get started! 🏁

---
# 2 - FLASH AN IMAGE <a name="2"></a>

> [!NOTE] 
>  An image with Raspberry PI OS Trixie Lite (64-bit) with default settings is pre-installed in the product. To test it first for the first time, go directly to the [chapter 3](#3).

## 2.1 Install the flashing tools on your computer <a name="2.1"></a>

To change the factory version or OS, you must first install the required tools on your computer.

The Official Raspberry Pi CM5 flashing documentation on the Compute Module CM5 IO Board is 👉 [here](https://www.raspberrypi.com/documentation/computers/compute-module.html#flash-compute-module-emmc)
with a tutorial video 👉 [here](https://www.youtube.com/watch?v=SWv-WYlHJWQ&t=44s)

Folow these tutorials to install **rpiboot** and **Raspberry Pi Imager** on your computer.

### 2.1.1 Use RPIBOOT on Mac <a name="2.1.1"></a>
```
brew install libusb pkg-config
```
check pkg-config
```
pkg-config --version
```
check libusb is well installed
```
ls /opt/homebrew/include/libusb-1.0/libusb.h
```
```
git clone https://github.com/raspberrypi/usbboot
```
```
cd usbboot
```
From inside the usbboot folder, run:
```
make CFLAGS="-I/opt/homebrew/include/libusb-1.0"

```
```
sudo ./rpiboot
```
## 2.2 Flash procedure <a name="2.2"></a>

> [!CAUTION]
>  Please note that with the Xplorer CM5 :
>  - the J2 jumper of the Officiel I/O board is replace with a **bootload switch under the left cap**.
>  - **This switch must be flip for the entire duration of the download**.
>  - The Xplorer CM5 is not powered via USB-C; it **must be powered via CAN1-PWR during the entire flashing process**.
>  - If your computer prompts you to format disks via pop-up windows during the flashing process, ignore and close them.

The flashing procedure is:
- Disconnect the USB-C cable
- Turn off the power via CAN1-PWR
- Remove the cap on the left side of the enclosure
- Flip the bootload switch under this cap toward the SMA connectors
- Power up via CAN1-PWR
- Launch **rpiboot** on your computer
```
RPIBOOT: build-date 2025/05/19 pkg-version local 402baf02

Please fit the EMMC_DISABLE / RPIBOOT jumper before connecting the power and USB cables to the target device.
If the device fails to connect then please see https://rpltd.co/rpiboot for debugging tips.
Waiting for BCM2835/6/7/2711/2712...
```
- Connect the USB-C cable
- In Windows, you should hear the USB driver notification sound
- **rpiboot** should detect Xplorer CM5 and read several files
```
Directory not specified - trying default /usr/share/rpiboot/mass-storage-gadget64/
read_file: Failed to read "2712/bootcode5.bin" from "/usr/share/rpiboot/mass-storage-gadget64/bootfiles.bin" - No such f
ile or directory
Trying local path mass-storage-gadget64/
Sending bootcode.bin
Successful read 4 bytes
Waiting for BCM2835/6/7/2711/2712...
Second stage boot server
File read: mcb. bin
File read: memsys00.bin
File read: memsys01.bin
File read: memsys02.bin
File read: memsys03.bin
File read: bootmain
Loading: mass-storage-gadget64//config.txt
File read: config.txt
Loading: mass-storage-gadget64//boot.img
File read: boot.img
```
- Launch **Raspberry Pi Imager** on your PC
- Select a Raspberry PI5/CM5 model
- Select your image :
    - RPI OS without desktop (Recommanded):
        - In raspberry Pi OS (Other) -> Raspberry PI OS Lite (64-bit) to select last Debian (Trixie factory delivery)
        - Or 👉 [here](https://downloads.raspberrypi.org/raspios_lite_arm64/images/) to select an old LTS RPI OS image
    - RPI OS with desktop :
        - Last Debian Trixie 64 bits
        - Or 👉 [here](https://downloads.raspberrypi.org/raspios_full_arm64/images/) to select an old LTS RPI OS image
    - Or in Other general-purpose OS -> Ubuntu to select an Ubuntu desktop or server Image
- Choose :
    - **mmcblk0** for eMMC (recommanded for the OS)
    - **nvme0n1** for the main NVMe SSD storage (you must change the boot order if you choose this drive)
- Configure the settings, the default factory settings are :
    - host: **xplorercm5.local**
    - User : **xplr**
    - Password : **changeme**
    - Wifi : yes
    - SSID : ************ (put your WIFI hotspot name)
    - Password : ************ (put your WIFI password)
    - ssh : yes
- Start flashing, it can last for several minutes ☕
- At the end of programming and verification
  - Disconnect the USB-C
  - Turn off the power via CAN1-PWR
  - Switch the switch back to the M12 connector direction
  - Put the cap back on
  - Power up via CAN1-PWR

---

# 3 - GETTING STARTED 🏁 <a name="3"></a>

## 3.1 - Launch a SSH console 🔐 <a name="3.1"></a>
Connect the Xplorer to your ethernet network, and verify the LEDs on your switch (Must indicate 1GbE).  
To get a DHCP defined IP address, you have multiples solutions :

**Solution 1 :** With a ping
```
ping -c 3 xplorercm5.local
```
```
PING xplorercm5.local (10.10.10.191): 56 data bytes
64 bytes from 10.10.10.191: icmp_seq=0 ttl=64 time=0.451 ms
```
**Solution 2 :** With a network scanning with [Angryip](https://angryip.org/)
```
...
10.10.10.191     18 ms    xplorercm5.ts.net lan    [n/a]
...
```
**Solution 3 :** Startup with a monitor connected to the Xplorer with a micro HDMI to HDMI (or mini HDMI) cable
```
...
You IP address is 10.10.10.191
...
```
**Solution 4 :** Open a putty console connected to COM1 at 115200 bauds
```
...
My IP address is 10.10.10.191
...
```
In our case our local Ethernet DHCP IP address is : 10.10.10.191

Open a ssh console using Ethernet with the IP address displayed :
```
ssh xplr@10.10.10.191
```
with the default password : **changeme**

> [!NOTE]  
> At the first connection you must accept the connection

```
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
```

> [!TIP]  
> After changing the hostname, you will have a message ending with
> ```Host key verification failed.```. Remove the problematic IP or hostname with 
> ```
> ssh-keygen -R 10.10.10.191
> ```
> and try to open a ssh console again.

> [!CAUTION]
> If you have an unconfigured Cellular M.2 module in place, you may have to wait one minute to have access to the ssh console via ethernet. In the worst case scenario, you may be blocked, retry a power-up or use ssh over WiFi, or a serial console on COM1, or a HDMI monitor and a keyboard in order to understand the problem and configure ModemManager.

## 3.2 - Update the linux and eeprom 🗓️ <a name="3.2"></a>
Update the package list, distribution, eeprom:
```
sudo apt --yes update && sudo apt --yes full-upgrade
sudo rpi-eeprom-update -a
```
And reboot:
```
sudo reboot
```
> [!CAUTION]
> If you have an unconfigured Cellular M.2 module in place, you may have to disable usb0 or ppp0 to have access to internet and make this update: ```sudo ip link set dev usb0 down``` or ```sudo ip link set dev ppp0 down```

## 3.3 - Patch the configuration file <a name="3.2"></a>

> [!NOTE]  
> If you have flashed a new image, you must configure the Xplorer CM5 peripherals.
> **This step is not necessary with the factory image**.

Edit config.txt :
```
sudo nano /boot/firmware/config.txt
```
Enable I2C and disable audio if you don't use it :
```
...
dtparam=i2c_arm=on
...
#dtparam=audio=on
...
[all]
```
And add at the end after [all] :
```
# Xplorer CM5 : TPM 2.0 (/dev/i2c-13)
dtoverlay=tpm-slb9673

# Xplorer CM5 : SPI DAQ
#dtoverlay=spi1-3cs
dtoverlay=spi1-3cs,cs0_spidev=off
#dtoverlay=mcp251xfd,spi1-0

# Xplorer CM5 : SPI CAN1 (can1)
dtoverlay=mcp251xfd,spi1-1,oscillator=40000000,interrupt=7

# Xplorer CM5 : SPI Isolated CAN2 (can0)
dtoverlay=mcp251xfd,spi1-2,oscillator=40000000,interrupt=10

# Xplorer CM5 : Option LoRa or Option IMU - Internal UART (ttyS0)
dtparam=uart0_console=off
dtparam=uart0=off
#dtparam=uart0=on

# Xplorer CM5 : COM1 RS232 (ttyAMA1)
enable_uart=1
dtoverlay=uart1

# Xplorer CM5 : COM2 RS232, Optional CTS/PPS (ttyAMA2)
dtoverlay=uart2
#dtoverlay=uart2,cts

# Xplorer CM5 : COM3 - Isolated RS232 mode (ttyAMA3)
dtoverlay=uart3
gpio=11=op,dl
dtparam=pwr_led_trigger=none
dtparam=pwr_led_activelow=off

# Xplorer CM5 : COM3 - XOR Isolated RS485 mode (ttyAMA3)
#dtoverlay=uart3,rts
#dtparam=pwr_led_trigger=none
#dtparam=pwr_led_activelow=on

# Xplorer CM5 : COM4 - Isolated Autodir RS485 (ttyAMA2)
dtoverlay=uart4

# Xplorer CM5 : micro SD Card
dtoverlay=sdio        

# Xplorer CM5 : External WiFi/BT Antenna
dtparam=ant2

# Xplorer CM5 : Charge the RTC Battery  
dtparam=rtc_bbat_vchg=3000000

# Xplorer CM5 : Activity LED to 1Hz blink or Heartbeat
#dtparam=act_led_trigger=timer
dtparam=act_led_trigger=heartbeat
dtparam=act_led_activelow=off

# Xplorer CM5 : Enable the watchdog
#dtparam=watchdog=on

# Xplorer CM5 with option MGM240PA32 : GPIO39 Control NRST, GPIO45 Control NBOOT
gpio=39=op,dh
gpio=45=op,dh

#========================================================
# Xplorer CM5 : Reduce the power consumption down to 2.8W
#========================================================

#--- No fan
#dtparam=cooling_fan=off

#--- Headless: Disable video outputs, reduce GPU RAM, Disable HDMI audio, GPU freq to mini
#hdmi_blanking=2
#display_default_lcd=0
#gpu_mem=4
#dtparam=audio=off
#gpu_freq=200
#dtoverlay=vc4-kms-v3d,noaudio
#dtoverlay=vc4-kms-v3d,nohdmi
#dtparam=hdmi=off

#--- Reduce Ethernet speed to 100MB (-0.25W)
#dtparam=eth_max_speed=100

#--- Disable unused RTC
#dtparam=rtc=off

#--- Disable unused Wireless
#dtoverlay=disable-wifi
#dtoverlay=disable-bt

#--- Disable Activity LEDs
#dtparam=act_led_trigger=none
#dtparam=act_led_activelow=off

#--- Disable SD card
#dtoverlay=disable-sdcard

#--- Underclocking & small undervolting (<=1.2Ghz)
#arm_freq=1200
#arm_freq_min=600
#gpu_freq=250
#over_voltage=-2

#--- Aggressive Underclocking & undervolting (<=1Ghz)
#arm_freq=1000
#arm_freq_min=400
#gpu_freq=200
#over_voltage=-5

#--- For low power SSD -> activate ASPM L0s/L1/L1.2
#pcie_aspm=force

#--- No PCIe M.2 modules -> Desactivate the PCIe switch (-1.3W)
#dtparam=pciex1=off

```
Usefull documentations to configure config.txt:
- [Config.txt](https://www.raspberrypi.com/documentation/computers/config_txt.html)
- [Device Tree Overlays](https://raw.githubusercontent.com/raspberrypi/firmware/master/boot/overlays/README)
- [Configure the Activity LED](https://raspberrypi.stackexchange.com/questions/69674/are-there-other-act-led-trigger-options-besides-mmc-and-heartbeat)

## 3.4 - Enable I2C <a name="3.4"></a>
Even with I2C enable in config.txt, ```sudo i2cdetect -l``` is not working without activating I2C in raspi-config.
```
sudo raspi-config nonint do_i2c 0
```
## 3.5 - Option : Activate a RS232 console <a name="3.5"></a>
To activate a console on the COM1 port to view the boot sequence and debug the network configuration. You need to replace ```console=serial0,115200``` with ```console=ttyAMA1,115200``` in ```/boot/firmware/cmdline.txt```. Note that ```console=tty1``` is for HDMI.

You can do it with :
```
sudo sed -i 's/serial0/ttyAMA1/g' /boot/firmware/cmdline.txt
```
And reboot if needed to apply now.
> [!TIP]
> To follow the log trace with date and time on a console, wired COM1 to a RS232 to USB Cable, open a putty terminal at 115200 Bauds on your computer, log and launch ```dmesg -Tw```

## 3.6 - Option : Static IP configuration <a name="3.6"></a>
Open the NetworkManager Configuration :
```
sudo nmcli connection show
```
Modify the Connection to Set a Static IP :
```
sudo nmcli connection modify "Wired connection 1" ipv4.addresses 192.168.1.100/24
sudo nmcli connection modify "Wired connection 1" ipv4.gateway 192.168.1.1
sudo nmcli connection modify "Wired connection 1" ipv4.dns "8.8.8.8 8.8.4.4"
sudo nmcli connection modify "Wired connection 1" ipv4.method manual
```
Replace 192.168.1.100 with your desired IP, and adjust the gateway and DNS settings as needed.
Save and Apply the Configuration :
```
sudo nmcli connection up "Wired connection 1"
```
Verify the Static IP:
```
ip addr show eth0
```
## 3.7 - Change Password <a name="3.7"></a>
The default password is **"changeme"**, to change it :
```
sudo passwd xplr
```
## 3.8 - Installation of usefull tools <a name="3.8"></a>
Install usefull tools to follow this tutorial and reboot :
```
sudo apt --yes install ethtool i2c-tools libtss2-* tpm-udev tpm2-abrmd tpm2-tools can-utils minicom
sudo usermod --append --groups tss $(whoami)
sudo reboot
```
> [!CAUTION]
> If you have an unconfigured Cellular M.2 module in place, you may have to disable usb0 or ppp0 to have access to internet: ```sudo ip link set dev usb0 down``` or ```sudo ip link set dev ppp0 down```

---
# 4 - TEST THE PERIPHERALS 🎓 <a name="4"></a>
## 4.1 - Linux configuration 💻 <a name="4.1"></a>
### Linux version :
```
uname -a
```
```
Linux xplorercm5 6.12.47+rpt-rpi-2712 #1 SMP PREEMPT Debian 1:6.12.47-1+rpt1 (2025-09-16) aarch64 GNU/Linux
```
### OS version :
```
cat /etc/os-release
```
```
PRETTY_NAME="Debian GNU/Linux 13 (trixie)"
...
```
### Debian version :
```
cat /etc/debian_version
```
```
13.2
```
## 4.2 - Ethernet <a name="4.2"></a>
### 4.2.1 - GbE over M12 <a name="4.2.1"></a>
```
sudo apt install ethtool
ethtool eth0
```
You should see:
```
...
Speed: 1000Mb/s
Duplex: Full
...
```
### 4.2.2 - 5 GbE over USB-C <a name="4.2.2"></a>
You can have an additional 5 GbE port with an external USB-C to 5Gbps Ethernet adapter.  
But you can have also a very high speed Vitual Network over USB-C with only a USB-C Cable, if you need only a P2P use :
- SSH console
- Remote Desktop like [Raspberry PI Connect](https://www.raspberrypi.com/software/connect/)
- Rapid retrieval of large data logs

Follow this [USB Ethernet Gadget Setup tutorial](https://ohyaan.github.io/tips/usb_ethernet_gadget_setup/#summary) to set up a USB Ethernet Gadget.

## 4.3 - WiFi/BT <a name="4.3"></a>
External antenna , config.txt
```
# Switch to external antenna.
dtparam=ant2
```
Params:
- ant1 : Select antenna 1 = internal (default)
- ant2 : Select antenna 2 = external
- noant: Disable both antennas

# <code style="color : RED">TBC</code>

##  4.4 - Serials <a name="4.4"></a>
List all the ports:
```
ls /dev/ttyA*
```
You should see 5 ports:
```
/dev/ttyAMA0  /dev/ttyAMA10  /dev/ttyAMA3
/dev/ttyAMA1  /dev/ttyAMA2   /dev/ttyAMA4
```
And:
```
ls -l /dev/ttyUSB*
```
You should see at least 4 ports:
```
/dev/ttyUSB0  /dev/ttyUSB1  /dev/ttyUSB2  /dev/ttyUSB3
```
ttyUSB0 to ttyUSB4 correspond to RXD_A to RXD_D
Note: You can see more ttyUSB depending of M.2 modules options (Cellular, GNSS...)
### 4.4.1 - UART0 <a name="4.4.1"></a>
This UART is used internaly by the options : LoRa/Sigfox xor IMU

⚠️ By default this port is in linux console mode, to deactivate the console and use as an UART, config.txt must contain :
```
dtparam=uart0_console=off
dtparam=uart0=on
```
Configure Baudrate:
```
stty -F /dev/ttyAMA0 speed 115200 cs8 -cstopb -parenb
```
Read Test :
```
cat /dev/ttyAMA0
```
Write Test :
```
echo -e "TX UART0 is Working\x0D\x0A" > /dev/ttyAMA0
```
### 4.4.2 - COM1 <a name="4.4.2"></a>
Configure Baudrate:
```
stty -F /dev/ttyAMA1 speed 115200 cs8 -cstopb -parenb
```
Read Test :
```
cat /dev/ttyAMA1
```
Write Test :
```
echo -e "TX COM1 Working \x0D\x0A" > /dev/ttyAMA1
```
### 4.4.3 - COM2 <a name="4.4.3"></a>
Configure Baudrate:
```
stty -F /dev/ttyAMA2 speed 115200 cs8 -cstopb -parenb
```
Read Test :
```
cat /dev/ttyAMA2
```
Write Test :
```
echo -e "TX COM2 Working \x0D\x0A" > /dev/ttyAMA2
```
### 4.4.4 - COM3 in RS232 Mode <a name="4.4.4"></a>
This port is an isolated dual-mode RS232 or RS485 port. By default, this port is in 3 wires RS232 mode (TXD, RXD, RTS).  
The power LED is used to select the mode RS232 or RS485.  
RTS/GPIO11 is used for the RS485 low impedance.  

In RS232 mode the config.txt must contain :
```
dtoverlay=uart3
gpio=11=op,dl
dtparam=pwr_led_trigger=none
dtparam=pwr_led_activelow=off
```
Configure Baudrate:
```
stty -F /dev/ttyAMA3 speed 115200 cs8 -cstopb -parenb
```
Read Test :
```
cat /dev/ttyAMA3
```
Write Test :
```
echo -e "TX COM3 is Working in RS232\x0D\x0A" > /dev/ttyAMA3
```
### 4.4.5 - COM3 in RS485 Mode <a name="4.4.5"></a>
In RS485 mode config.txt must contain :
```
dtoverlay=uart3,rts
dtparam=pwr_led_trigger=none
dtparam=pwr_led_activelow=on
```
To send a sentence using RTS controlling DE, test with a basic python script :
```
import serial
from serial.rs485 import RS485Settings

ser = serial.Serial('/dev/ttyAMA3', baudrate=19200, timeout=0.1)
ser.rs485_mode = RS485Settings(
    rts_level_for_tx=True,
    rts_level_for_rx=False,
    rts_before_send=0.0005,
    rts_after_send=0.0005
)
ser.write(b'TX COM3 is Working in RS485\x0D\x0A')
ser.flush()
```
### 4.4.6 - COM4 <a name="4.4.6"></a>
COM4 is an half duplex RS485 port with AutoDirection Control (No DE via RTS to command Transmit low impedance). Configure Baudrate:
```
stty -F /dev/ttyAMA4 speed 19200 cs8 -cstopb -parenb
```
Read Test :
```
cat /dev/ttyAMA4
```
Write Test :
```
echo -e "TX COM4 Working \x0D\x0A" > /dev/ttyAMA4
```
### 4.4.7 - RXDA <a name="4.4.7"></a>
```
stty -F /dev/ttyUSB0 speed 115200 cs8 -cstopb -parenb
```
Read Test :
```
cat /dev/ttyUSB0
```
### 4.4.8 - RXDB <a name="4.4.8"></a>
⚠️ IN1_RXDB is not functional with the **Matter** hardware option
```
stty -F /dev/ttyUSB1 speed 115200 cs8 -cstopb -parenb
```
Read Test :
```
cat /dev/ttyUSB1
```
### 4.4.9 - RXDC <a name="4.4.9"></a>
```
stty -F /dev/ttyUSB2 speed 115200 cs8 -cstopb -parenb
```
Read Test :
```
cat /dev/ttyUSB2
```
### 4.4.10 - RXDD <a name="4.4.10"></a>
```
stty -F /dev/ttyUSB3 speed 115200 cs8 -cstopb -parenb
```
Read Test :
```
cat /dev/ttyUSB3
```
## 4.5 - CAN-FD <a name="4.5"></a>
### 4.5.1 - SPI <a name="4.5.1"></a>
```
dmesg | grep -i -E "(mcp|spi)"
```
```
...
[    5.936984] mcp251xfd spi1.2 can0: MCP2518FD rev0.0 (-RX_INT -PLL -MAB_NO_WARN +CRC_REG +CRC_RX +CRC_TX +ECC -HD o:40.00MHz c:40.00MHz m:20.00MHz rs:17.00MHz es:16.66MHz rf:17.00MHz ef:16.66MHz) successfully initialized.
[    5.946398] mcp251xfd spi1.1 can1: MCP2518FD rev0.0 (-RX_INT -PLL -MAB_NO_WARN +CRC_REG +CRC_RX +CRC_TX +ECC -HD o:40.00MHz c:40.00MHz m:20.00MHz rs:17.00MHz es:16.66MHz rf:17.00MHz ef:16.66MHz) successfully initialized.
...
```
You must see can0 and can1 usign MCP2518FD chipset on SPI1
```
ifconfig -a
```
```
can0: flags=128<NOARP>  mtu 16
        unspec 00-00-00-00-00-00-00-00-00-00-00-00-00-00-00-00  txqueuelen 10  (UNSPEC)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
        device interrupt 197  

can1: flags=128<NOARP>  mtu 16
        unspec 00-00-00-00-00-00-00-00-00-00-00-00-00-00-00-00  txqueuelen 10  (UNSPEC)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
        device interrupt 198 
... 
```
You must see **can0** and **can1**
### 4.5.2 - CAN1 <a name="4.5.2"></a>
To configure the main CANBus 'can1' on CAN1/PWR connector (NMEA2000 compatible):
```
sudo apt-get install can-utils
sudo ip link set can1 up type can bitrate 250000
```
Test the reception with : 
```
candump can1
```
Send a sentence with :
```
cansend can1 7DF#0201050000000000
```
### 4.5.3 - CAN2 <a name="4.5.3"></a>
To configure the secondary CANbus 'can0' on DAQ/CAN2 connector:
```
sudo apt-get install can-utils
sudo ip link set can0 up type can bitrate 250000
```
Test the reception with : 
```
candump can0
```
Send a sentence with :
```
cansend can0 7DF#0201050000000000
```

## 4.6 - CyberSecurity <a name="4.6"></a>
### 4.6.1 - I2C <a name="4.6.1"></a>
Enable I2C (raspi-config -> Interface options -> I2C -> Enable):
```
sudo raspi-config
```
If needed valid also the I2C in config.txt :
```
echo "dtparam=i2c_arm=on" | sudo tee -a /boot/firmware/config.txt
sudo reboot
```
> [!NOTE]
> In the Raspberry Pi documentation, the raspi-config I2C enable has the same effect as enabling I2C in config.txt and reboot. Experimentally, you need to do raspi-config to list I2C devices. 

and:
```
sudo apt-get install i2c-tools
```
List I2C & TPM devices and I2C pilot :
```
sudo i2cdetect -l|sort && i2cdetect -y -r 13 && ls -l /dev/tpm* && lsmod | grep i2c
```
Shows this:
```
i2c-13	i2c       	i2c-gpio@1                      	I2C adapter
i2c-14	i2c       	107d508200.i2c                  	I2C adapter
i2c-15	i2c       	107d508280.i2c                  	I2C adapter
     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
00:                         -- -- -- -- -- -- -- -- 
10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
20: -- -- -- -- -- -- -- -- -- -- -- -- -- -- UU -- 
30: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
40: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
50: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
60: 60 -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
70: -- -- -- -- -- -- -- --                         
crw-rw---- 1 tss root  10,   224 Jan 12 15:41 /dev/tpm0
crw-rw---- 1 tss tss  510, 65536 Jan 12 15:41 /dev/tpmrm0
tpm_tis_i2c            49152  0
crc_ccitt              49152  1 tpm_tis_i2c
tpm_tis_core           65536  1 tpm_tis_i2c
tpm                    98304  4 tpm_tis_i2c,tpm_tis_core
i2c_brcmstb            49152  0
i2c_gpio               49152  0
i2c_algo_bit           49152  1 i2c_gpio
i2c_dev                49152  0
```
TPM2.0 with the SLB9673AU20FW2610XTMA1 : Adr 2E -> 0x2E or UU
Option CryptoAuthentication with the ATECC608A-MAHDA : Adr 0x60 -> 0x60 or UU

[I2C Tools Tutorial](https://emlogic.no/2025/06/accessing-i2c-devices-from-userspace-in-linux/)

### 4.6.2 - TPM2.0 <a name="4.6.2"></a>

This feature uses the [Infineon OPTIGA SLB9673AU20FW2610XTMA1](https://www.infineon.com/assets/row/public/documents/30/49/infineon-slb9673-tpm20-i2c-fw26xx-ds-rev1-4-2024-11-13-datasheet-en.pdf) TPM2.0 I2C Chip with 51KB of NV memory.

Documentation : 
- [OPTIGA TPM RPi Quickstarter User Guide](https://www.infineon.com/gated/infineon-optiga-tpm-rpi-quickstarter-user-guide-usermanual-en_a3d6e6e3-6da2-4321-816d-8c6bcddc55ee)
- [Hardware Security Module (TPM) Setup with dm-verity and Encrypted Storage ](https://ohyaan.github.io/tips/hardware_security_module__tpm__setup_with_dm-verity_and_encrypted_storage/#installing-tpm-hardware)

If needed, add this line in config.txt and reboot
```
sudo nano /boot/firmware/config.txt
```
Verify this settings:
```
dtoverlay=tpm-slb9673
```
Then check the driver :
```
ls -l /dev/tpm*
```
shows:
```
crw------- 1 root root  10,   224 Aug  4 15:02 /dev/tpm0
crw------- 1 root root 509, 65536 Aug  4 15:02 /dev/tpmrm0
```
If needed, install the TPM libraries and tools and reboot:
```
sudo apt --yes install libtss2-* tpm-udev tpm2-abrmd tpm2-tools
sudo usermod --append --groups tss $(whoami)
sudo reboot
```
Check the TPM2.0 Interface with :
```
tpm2 getcap properties-fixed
```
Displays TPM status:
```
TPM2_PT_FAMILY_INDICATOR:
  raw: 0x322E3000
  value: "2.0"
TPM2_PT_LEVEL:
  raw: 0
...
```
And follow this [infineon tutorial for more informations](https://www.infineon.com/assets/row/public/documents/30/44/infineon-optiga-tpm-rpi-quickstarter-user-guide-usermanual-en.pdf)

### 4.6.3 - CrytoAuthentication Co-Processor <a name="4.6.3"></a>
This option uses the [Microchip ATECC608A-MAHDA](https://ww1.microchip.com/downloads/aemDocuments/documents/SCBU/ProductDocuments/DataSheets/ATECC608A-CryptoAuthentication-Device-Summary-Data-Sheet-DS40001977B.pdf) I2C Chip with 16 keys storage, Asymmetric & Symmetric Algorithms, Networking Key Management, Secure boot, 72 bits Unique ID...

Documentations :
- [Github atecc-util](https://github.com/wirenboard/atecc-util)
- [ATECC608A I2C Notes](https://gist.github.com/jj1bdx/ad2dedcbacb9198bd4e1667008e9dbe5)
- [Application note](https://ww1.microchip.com/downloads/aemDocuments/documents/OTH/ApplicationNotes/ApplicationNotes/Atmel-8983-CryptoAuth-ATECC508A-Node-Example-Asymmetric-PKI-ApplicationNote.pdf)
- [Secure boot using ATECC608A](https://forums.raspberrypi.com/viewtopic.php?t=353718)

```
sudo apt-get install git debhelper
git clone https://github.com/contactless/atecc-util
cd atecc-util
git submodule init
git submodule update
make
dpkg-buildpackage
```
Check the CrytoAutentification interface getting the unique ID on /dev/i2c-13 
```
~/atecc-util/atecc -b 13 -c 'serial'
```
Displays a Unique ID:
```
0123ceb0b0dbc3d2ee
```
## 4.7 - Storages <a name="4.7"></a>
### 4.7.1 - PCIe peripherals <a name="4.7.1"></a>
The 'lspci' command must discover the ASM1184e PCIe switch and equiped M.2 modules (below with one KIOXIA SSDs and one Hailo-8 AI module).
```
lspci
```
```
0001:00:00.0 PCI bridge: Broadcom Inc. and subsidiaries BCM2712 PCIe Bridge (rev 30)
0001:01:00.0 PCI bridge: ASMedia Technology Inc. ASM1184e 4-Port PCIe x1 Gen2 Packet Switch
0001:02:01.0 PCI bridge: ASMedia Technology Inc. ASM1184e 4-Port PCIe x1 Gen2 Packet Switch
0001:02:03.0 PCI bridge: ASMedia Technology Inc. ASM1184e 4-Port PCIe x1 Gen2 Packet Switch
0001:02:05.0 PCI bridge: ASMedia Technology Inc. ASM1184e 4-Port PCIe x1 Gen2 Packet Switch
0001:02:07.0 PCI bridge: ASMedia Technology Inc. ASM1184e 4-Port PCIe x1 Gen2 Packet Switch
0001:03:00.0 Non-Volatile memory controller: KIOXIA Corporation NVMe SSD Controller BG4
0001:06:00.0 Co-processor: Hailo Technologies Ltd. Hailo-8 AI Processor (rev 01)
0002:00:00.0 PCI bridge: Broadcom Inc. and subsidiaries BCM2712 PCIe Bridge (rev 30)
0002:01:00.0 Ethernet controller: Raspberry Pi Ltd RP1 PCIe 2.0 South Bridge
```
### 4.7.2 - USB peripherals <a name="4.7.2"></a>
The 'lsusb' command must discover the FT4232H (USB2<->4x UART chip), equiped M.2 type B modules (below a 5G Qualcomm M.2 module) and external USB-C device if connected.
```
lsusb
```
```
Bus 001 Device 002: ID 1e0e:9001 Qualcomm / Option SimTech, Incorporated
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 005 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 004 Device 002: ID 0403:6011 Future Technology Devices International, Ltd FT4232H Quad HS USB-UART/FIFO IC
Bus 004 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 003 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```
### 4.7.3 - Drives <a name="4.7.3"></a>
```
lsblk
```
```
NAME         MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
mmcblk0      179:0    0  29.1G  0 disk 
├─mmcblk0p1  179:1    0   512M  0 part /boot/firmware
└─mmcblk0p2  179:2    0  28.6G  0 part /
mmcblk0boot0 179:32   0     4M  1 disk 
mmcblk0boot1 179:64   0     4M  1 disk 
mmcblk2      179:96   0  29.7G  0 disk 
├─mmcblk2p1  179:97   0   256M  0 part /media/xxxx/boot
└─mmcblk2p2  179:98   0  29.5G  0 part /media/xxxx/rootfs
nvme0n1      259:0    0 119.2G  0 disk
nvme1n1      259:1    0 931.5G  0 disk
```
- **mmcblk0** is the CM5 eMMC, here with 2 partitions
- **mmcblk2** is the optional uSD card, here with 2 partitions
- **nvme0n1** is the optional main NVMe SSD
- **nvme1n1** is the optional secondary NVMe SSD
- **sda1** would have been an optional USB-C flash drive
### 4.7.4 - Type-C External Flash Drive  <a name="4.7.4"></a>
This test show you how to test a USB3 peripheral, it is made with a small USB-C key connected to the USB-C, it uses the [Samsung MUF-64DA/PAC](https://www.samsung.com/uk/memory-storage/usb-flash-drive/usb-flash-drivetype-c-64gb-muf-64da-apc/) (64GB, USB3.1, <300MB/S read speed, reversible ports, formated in FAT, Waterproof)
```
lsusb
```
```
...
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 005 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 004 Device 002: ID 0403:6011 Future Technology Devices International, Ltd FT4232H Quad HS USB-UART/FIFO IC
Bus 004 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 003 Device 002: ID 04e8:6300 Samsung Electronics Co., Ltd Type-C
Bus 003 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
...
```
⚠️ You must see the "Samsung Electronics Co., Ltd Type-C" device and "Linux Foundation 3.0" for USB 3.0 peripherals
```
lsusb -t | grep xhci
```
```
/:  Bus 05.Port 1: Dev 1, Class=root_hub, Driver=xhci-hcd/1p, 5000M
/:  Bus 04.Port 1: Dev 1, Class=root_hub, Driver=xhci-hcd/2p, 480M
/:  Bus 03.Port 1: Dev 1, Class=root_hub, Driver=xhci-hcd/1p, 5000M
/:  Bus 02.Port 1: Dev 1, Class=root_hub, Driver=xhci-hcd/2p, 480M
```
⚠️ Idem, you must see "5000M" for USB3.0 Peripherals.  

To check USB version of your disk, here 3.10 :
```
sudo lsusb -v 2>/dev/null | grep -e "^Bus\|bcdUSB"
```
```
...
Bus 003 Device 002: ID 04e8:6300 Samsung Electronics Co., Ltd Type-C
  bcdUSB               3.10
...
```
Get disk size and name :
```
lsblk -D
```
```
NAME         DISC-ALN DISC-GRAN DISC-MAX DISC-ZERO
sda                 0      512B       0B         0
└─sda1              0      512B       0B         0
mmcblk0             0        4M     2.2G         0
├─mmcblk0p1         0        4M     2.2G         0
└─mmcblk0p2         0        4M     2.2G         0
mmcblk0boot0        0        4M     2.2G         0

```
Get mounting status:
```
sudo cat /proc/mounts
```
```
...
/dev/sda1 /media/xplr/Samsung\ USB vfat rw,nosuid,nodev,relatime,uid=1000,gid=1000,fmask=0022,dmask=0022,codepage=437,iocharset=ascii,shortname=mixed,showexec,utf8,flush,errors=remount-ro 0 0
...
```
```
cd /media/xplr/Samsung\ USB/
ls -l
```
```
ls -l /dev/disk/by-uuid
```
```
total 0
lrwxrwxrwx 1 root root 10 Aug  1 14:20 3FFA-6704 -> ../../sda1
lrwxrwxrwx 1 root root 15 Jul 26 16:17 d6ecfcd5-2703-41bf-9301-10c403b6fb0c -> ../../mmcblk0p2
lrwxrwxrwx 1 root root 15 Jul 26 16:17 F737-8E10 -> ../../mmcblk0p1
```
```
df -h
```
```
...
/dev/sda1        60G  3.5M   60G   1% /media/xplr/Samsung USB
...
```
```
sudo fdisk -l
```
```
...
Disk /dev/sda: 59.75 GiB, 64160400896 bytes, 125313283 sectors
Disk model: Type-C          
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x00000000
Device     Boot Start       End   Sectors  Size Id Type
```
```
sudo blkid /dev/sda1
```
```
/dev/sda1: LABEL="Samsung USB" UUID="3FFA-6704" BLOCK_SIZE="512" TYPE="vfat"
```
Benchmark the Type-C USB Flash Drive read speed:
```
sudo apt-get install hdparm
sudo hdparm -tT --direct /dev/sda1
```
```
/dev/sda1:
 Timing O_DIRECT cached reads:   494 MB in  2.01 seconds = 246.22 MB/sec
 Timing O_DIRECT disk reads: 546 MB in  3.00 seconds = 181.89 MB/sec
```
```
sudo dd bs=10M count=500 if=/dev/sda1 of=/home/xplr/test.bin
```
```
...
5242880000 bytes (5.2 GB, 4.9 GiB) copied, 42.4844 s, 123 MB/s
```
Benchmark the Type-C USB Flash Drive write speed:
```
sudo dd bs=2M count=500 if=/dev/sda1 of=/media/xplr/Samsung\ USB/test.bin
```
```
...
1048576000 bytes (1.0 GB, 1000 MiB) copied, 34.7954 s, 30.1 MB/s
```
### 4.7.5 - Internal NVMe SSD(s) <a name="4.7.5"></a>
- The main SSD is a 2232 Key M, M.2 module installed on the J15 slot (CM5 / Front side).
- To make a Raid 0 or 1 NAS, another 2232/2242 Key M, M.2 SSD can be installed on the J4 slot (Bottom plate side).
- A third 2232/2242 Key B, M.2 SSD can also be used if needed.

To list all the drives :
```
lsblk
```
```
NAME         MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
loop0          7:0    0     2G  0 loop 
mmcblk0      179:0    0  29.1G  0 disk 
├─mmcblk0p1  179:1    0   512M  0 part /boot/firmware
└─mmcblk0p2  179:2    0  28.6G  0 part /
mmcblk0boot0 179:32   0     4M  1 disk 
mmcblk0boot1 179:64   0     4M  1 disk 
zram0        254:0    0     2G  0 disk [SWAP]
nvme0n1      259:0    0 238.5G  0 disk        <---- Main SSD here
nvme1n1      259:1    0 931.5G  0 disk        <---- secondary SSD here
```
Benchmark the main SSD, here a Samsung P991a 256GB SSD :
```
sudo apt-get install hdparm
sudo hdparm -tT --direct /dev/nvme0n1
```
```
/dev/nvme0n1:
 Timing O_DIRECT cached reads:   822 MB in  2.00 seconds = 410.07 MB/sec
 Timing O_DIRECT disk reads: 1254 MB in  3.00 seconds = 417.77 MB/sec
```
```
sudo dd bs=10M count=500 if=/dev/nvme0n1 of=/home/xplr/test.bin
```
```
500+0 records in
500+0 records out
5242880000 bytes (5.2 GB, 4.9 GiB) copied, 35.8162 s, 146 MB/s
```
Benchmark the secondary SSD, here a Crucial P310 1TB SSD :
```
sudo hdparm -tT --direct /dev/nvme1n1
```
```
/dev/nvme1n1:
 Timing O_DIRECT cached reads:   838 MB in  2.00 seconds = 418.61 MB/sec
 Timing O_DIRECT disk reads: 1250 MB in  3.00 seconds = 416.10 MB/sec
```
```
sudo dd bs=10M count=500 if=/dev/nvme1n1 of=/home/xplr/test.bin
```
```
500+0 records in
500+0 records out
5242880000 bytes (5.2 GB, 4.9 GiB) copied, 47.4714 s, 110 MB/s
```
### 4.7.6 - Micro SD Card  <a name="4.7.6"></a>
An internal micro SD card holder is connected to GPIO22 to GPIO27.
An optional SD card may be use for non-critical storage or but it is rather intended for cybersecurity (Secure Acces Key, Hidden partition, Write Once Read Many).
To physically access to the push pull holder, you must remove the cap on the left side of the enclosure.
The side of the SD with the electrical contacts must be on the side of the PCB, here it's the side of the bottom plate, so the printed side of the SD is facing the front.
> [!CAUTION]
> It is possible to insert the SD card next to the holder and lose it inside the enclosure. The card must be inserted using small pliers, with the power turned off and easy access so you can see what you are doing.
> The cap must be lightly greased with vaseline after each opening to ensure a good seal.  

To access it in software, you must have in config.txt :
```
dtoverlay=sdio
```
To list the drives :
```
$ lsblk
...
mmcblk2      179:96   0  29.7G  0 disk 
├─mmcblk2p1  179:97   0   256M  0 part /media/xplr/boot
└─mmcblk2p2  179:98   0  29.5G  0 part /media/xplr/rootfs
...
```
**mmcblk2** is the uSD, here with 2 partitions
> [!TIP]
> To backup the eMMC on SD:
> ```
> sudo dd if=/dev/mmcblk0 of=/dev/mmcblk2 bs=4M status=progress
> ```
> To clone the SD to the main SSD:
> ```
> sudo dd if=/dev/mmcblk2 of=/dev/nvme0n1 bs=4M status=progress
> ```
## 4.8 - DAQ <a name="4.8"></a>
The **DAQ** uses the chip Analog Device [AD5592R](https://www.analog.com/media/en/technical-documentation/data-sheets/ad5592r.pdf), a 8-Channel (IO1 to IO7), 12-Bit, configurable ADC/DAC/GPIO with On-Chip 20 ppm/°C reference and a SPI interface connected to the SPI1.0  
It has a total throughput rate of 400 kSPS and an integrated temperature indicator.

# <code style="color : RED">TBC</code>

Usefull documentation:
- [Analog Device AD5592R IIO DAC/ADC Linux Driver](https://wiki.analog.com/resources/tools-software/linux-drivers/iio-dac/ad5592r)
- [Analog Device EVAL-AD5592R-PMDZ Overview](https://wiki.analog.com/resources/eval/user-guides/circuits-from-the-lab/eval-ad5592r-pmdz)
- [Analog Device AD5592R Driver doxygen doc](https://analogdevicesinc.github.io/no-OS/doxygen/dir_aa577ad46a7e19fba00f09ae0610f4c0.html)
- [Analog Device pyadi-iio](https://analogdevicesinc.github.io/pyadi-iio/devices/adi.ad5592r.html)
- [ADALM2000/AD5592R Device tree](https://github.com/adisuciu/m2kirl/blob/main/dt/rpi-ad5592r-m2kirl.dts)
- [AD5592R Linux driver](https://github.com/torvalds/linux/blob/master/drivers/iio/dac/ad5592r.c)
- [Video: Add Analog IO to #RPi with SpazzTech AD5592 Snack Board](https://www.youtube.com/watch?v=jSnT0_RSBUk)
- [Github AD5592_Snack_Board](https://github.com/SpazzTech/AD5592_Snack_Board)
- [AD5592R ROS2 Integration](https://docs.ros.org/en/rolling/p/adi_iio/doc/Examples/02_example_ad5592r.html)

## 4.9 - Cellular and Direct-To-Cell <a name="4.9"></a>
### 4.9.1 - Nano SIM <a name="4.9.1"></a>
The right cap provides access to a Push Pull holder for a nano SIM card or a 4FF Plastic eSIM card.
> [!CAUTION]
> It is possible to insert the SIM card next to the holder and lose it inside the enclosure. The card is inserted using small pliers, with the power turned off and easy access so you can see what you are doing.
> The cap must be lightly greased with vaseline after each opening to ensure a good seal. 
### 4.9.2 - 4FF eSIM <a name="4.9.2"></a>
An eSIM card can be integrated into production, and plugs can be removed for mass-produced products.  
[Kigen SGP.22+ Tri-cut eUICC eSIM](https://techship.com/product/kigen-sgp-22-tri-cut-e-uicc-e-sim/?variant=001)  
[How to use an eSIM in Linux?](https://techship.com/blog/how-to-use-an-esim-in-linux-7/)
### 4.9.3 - 4G LTE-A <a name="4.9.3"></a>
[Configure a Cellular / Direct-To-Cell modem with ModemManager](https://github.com/austral-electronics/Xplorer/blob/main/doc/Xplorer_CM5_Cellular_Modem_With_ModemManager.md)  
[Configure the QUECTEL EM060K-GL 4G LTE-A modem without ModemManager](https://github.com/austral-electronics/Xplorer/blob/main/doc/XplorerCM5_EM060K-GL_Without_ModemManager.md)
### 4.9.4 - 5G RedCap <a name="4.9.4"></a>
[Configure a Cellular / Direct-To-Cell modem with ModemManager](https://github.com/austral-electronics/Xplorer/blob/main/doc/Xplorer_CM5_Cellular_Modem_With_ModemManager.md)  
[Configure the SIM8230G 5G RedCap Modem without ModemManager](https://github.com/austral-electronics/Xplorer/blob/main/doc/XplorerCM5_SIM8230G_Without_ModemManager.md)
### 4.9.5 - Speed Test <a name="4.9.5"></a>
Install the [OOKLA speed test](https://www.speedtest.net/apps/cli) tool with :
```
sudo apt update
sudo apt install -y curl gnupg
curl -fsSL https://packagecloud.io/ookla/speedtest-cli/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/ookla.gpg
echo "deb [signed-by=/usr/share/keyrings/ookla.gpg] https://packagecloud.io/ookla/speedtest-cli/debian/ trixie main" | sudo tee /etc/apt/sources.list.d/ookla.list
sudo apt install -y speedtest
```
And launch:
```
speedtest --interface usb0
```
We get with a 4G plan SIM card:
```
Server:          ORANGE FRANCE - Paris (id: 62493)
ISP:             Bouygues Telecom
Idle Latency:    39.99 ms   (jitter: 7.99ms, low: 32.02ms, high: 47.98ms)
Download:        17.45 Mbps (data used: 29.6 MB)                                                   
                 247.88 ms  (jitter: 67.64ms, low: 51.55ms, high: 1166.13ms)
Upload:          8.77 Mbps  (data used: 14.7 MB)                                                   
                 861.83 ms  (jitter: 91.22ms, low: 49.22ms, high: 1839.04ms)
Packet Loss:     0.0%
```
## 4.10 - Multi-Protocol Wireless Network co-processor <a name="4.10"></a>
This option gives automation and IoT 2.4Ghz connectivity with Matter-Over-Thread, Zigbee, BLE Mesh and Open Thread.  
It's the perfect interface to make a Home Assistant Matter/Zibee Hub/Device or for custom Mesh communication.  
This option add to the BOM a [MGM240PA32VNN3](https://cdn.sparkfun.com/assets/1/4/5/e/5/MGM240P-Datasheet.pdf) module connected the LPWAN SMA connector for a 2.4 Ghz Antenna.  
Note that this option removes one RS232 input. 
The MGM240PA32VNN3 module includes a Silicon Lab EFR32MG24 Chip, the same as various USB dongles like [Home Assistant Connect ZBT-2](https://support.nabucasa.com/hc/en-us/articles/31313065259421-About-Home-Assistant-Connect-ZBT-2), [SONOFF Dongle Plus MG24](https://sonoff.tech/products/sonoff-zigbee-thread-usb-dongle-dongle-plus-mg24), or [smlight SLZB-07Mg24](https://smlight.tech/global/slzb07mg24).

### 4.10.1 - Software development <a name="4.10.1"></a>
For more information about the EFR32MG24 :
[EFR32MG24 Website](https://docs.zephyrproject.org/latest/boards/seeed/xiao_mg24/doc/index.html)
[EFR32MG24 Datasheet](https://www.silabs.com/documents/public/data-sheets/efr32mg24-datasheet.pdf)
[EFR32xG24 Reference Manual](https://www.silabs.com/documents/public/reference-manuals/brd4187c-rm.pdf)

The Xplorer CM5 hardware as no embbeded J-LINK OB Debugger but as an embedded UART Xmodem bootloader.
To debug your software you can use a external dev kit connected to the USB-C, like the [Sparkfun Thing Plus Matter Kit](https://www.sparkfun.com/sparkfun-thing-plus-matter-mgm240p.html), the [EFR32xG24 Explorer Kit](https://www.silabs.com/documents/public/user-guides/ug533-xg24-ek2703a.pdf), or the [XIAO MG24](https://www.seeedstudio.com/Seeed-Studio-XIAO-MG24-p-6247.html).
Only the name of the USB port will be changed for production.

### 4.10.2 - Pre-build Firmware <a name="4.10.2"></a>

#### Firmware Builds for dongles
https://github.com/NabuCasa/silabs-firmware-builder
https://github.com/darkxst/silabs-firmware-builder/tree/main
https://github.com/darkxst/silabs-firmware-builder/tree/main/firmware_builds
https://github.com/darkxst/silabs-firmware-builder/tree/main/firmware_builds/mgm240p

#### Firmware examples
https://github.com/NabuCasa/silabs-firmware

### 4.10.3 - UART Xmodem Bootload <a name="4.10.3"></a>

Your Linux application can manage the update of the MG24 firmware using an embedded UART Xmodem bootloader.  
The interface with the CM5 is achieved via a USB to UART converter and 2 pins on the CM5 to control the reset and bootload pins.  
The pinout is compliant with the Network Co-Processor (NCP) Application with UART in order to make a Matter or Zigbee Hub, see page 34 of the [MGM240PA32VNN3](https://cdn.sparkfun.com/assets/1/4/5/e/5/MGM240P-Datasheet.pdf).  

|MGM240 Pin|MG24 I/O| Connected to      | GPIO Name       | Name             | Description|                                                                        
|----------|--------|-------------------|-----------------|------------------|------------|
| 4        | PB02   | CM5 Pin 19        | FAN_PWM /GPIO45 | **NBOOT_MP_RAD** | MG24 Bootload pin
| 6        | PB00   | CM5 Pin 19        | FAN_PWM /GPIO45 | **NBOOT_MP_RAD** | MG24 Bootload pin
| 11       | PA04   | TP21              | TP21            | **TP21**         | Test Point (Reserved for a LED activated at low level in future PCB Revision) 
| 12       | PA05   | FT432H-56Q Pin 23 | BDBUS1          | **RXD_B**        | MG24 USART1.TX (Xmodem & NCP Compliant)  
| 13       | PA06   | FT432H-56Q Pin 21 | BDBUS0          | **TXD_B**        | MG24 USART1.RX (Xmodem & NCP Compliant)
| 16       | PA07   | FT432H-56Q Pin 25 | BDBUS3          | **CTS_B**        | MG24 (NCP Compliant)
| 17       | PA08   | FT432H-56Q Pin 24 | BDBUS2          | **RTS_B**        | MG24 (NCP Compliant)
| 31       | #RESET|  CM5 Pin 80        | SCL0 / GPIO39   | **NRST_MP_RAD**  | MG24 Reset

#### 4.10.3.1 - Define the bootloader activation pin <a name="4.10.3.1"></a>

The bootloader entry pin is user-defined and configured inside the Gecko Bootloader project.  
This must be done in the Gecko bootloader project, not in the application.  

In Simplicity Studio:  
Software Components  
→ Bootloader Core  
→ GPIO Activation (or Bootloader Button)  

Configure the NBOOT GPIO to PB00 or PB02 :  
- Port (gpioPortA, gpioPortB, …)
- Pin number
- Active level (HIGH or LOW)
- Pull configuration

Example:
```
Port        : gpioPortB
Pin         : 0
Active when : LOW
Pull        : Pull-up
```

Simplicity Studio auto-generates this (You don't need to write this manually):
```
#define BTL_BUTTON_PORT gpioPortB
#define BTL_BUTTON_PIN  0
#define BTL_BUTTON_PRESSED 0  // active low

if (GPIO_PinInGet(BTL_BUTTON_PORT, BTL_BUTTON_PIN)
    == BTL_BUTTON_PRESSED) {
    enterBootloader();
}
```

#### 4.10.3.2 - Command NRST and NBOOT <a name="4.10.3.2"></a>

To control NRST and NBOOT, config.txt must contain :
```
# Xplorer CM5 with option MGM240PA32 : GPIO39 Control NRST, GPIO45=FAN_PWM Control NBOOT
gpio=39=op,dh
gpio=45=op,dh
```
You can Reset the MG24 with :
```
pinctrl set 39 op pn dl
sleep .1
pinctrl set 39 op pn dh
```
You cant put the EFR32MG24 in bootload mode with the sequence :
 - NBOOT=0
 - NRST=0
 - Wait 100ms to reset the EFR32MG24
 - NRST=1
 - Wait 200ms to enter in bootload mode
 - NBOOT=1

The MG24 boot sequence can be made in command line with :
```
pinctrl set 45 op pn dl
pinctrl set 39 op pn dl
sleep .1
pinctrl set 39 op pn dh
sleep .2
pinctrl set 45 op pn dh
```
#### 4.10.3.3 - Flash manually using Minicom <a name="4.10.3.3"></a>
Install and minicom :
```
sudo apt-get install minicom
```
Put a gbl file to flash in the current directory (here a Zigbee NCP for Sparkfun)
```
wget https://github.com/darkxst/silabs-firmware-builder/releases/download/20250220/mgm240p_zigbee_ncp_8.0.2.0_sw_flow_115200.gbl
```
Open a console on ttyUSB1 (RXD_B) at 115Kbps with :
```
sudo minicom -D /dev/ttyUSB1 -b 115200
```
Send the boot sequence above.
After this sequence, the EFR32MG24 bootloader must send the message to the minicom terminal :
```
Gecko Bootloader v2.00.00
1. upload gbl
2. run
3. ebl info
BL >
```
Press 1 to begin the upload
```
begin upload                                                                    
CCCC
```
Press Ctrl + A an then S to select the minicom upload mode in the pop up menu :
```
+-[Upload]--+                                      
| zmodem    |                                      
| ymodem    |                                      
| xmodem    |                                      
| kermit    |                                      
| ascii     |                                      
+-----------+ 
```
Select 'xmodem'.  
Select your .gbl firmware to flash with the arrows, space and enter.
You will see a pop up window :
```
+----------------[xmodem upload - Press CTRL-C to quit]----------------+    
|Sending mgm240p_zigbee_ncp_8.0.2.0_sw_flow_115200.gbl, 2117 blocks: Gi|    
|ve your local XMODEM receive command now.                             |    
|Xmodem sectors/kbytes sent: 808/101k                                  |
+----------------------------------------------------------------------+   
```
And aftert few seconds
```
|Transfert completed                                                   |
```
#### 4.10.3.4 - Firmware update with the NabuCasa Universal Silicon Labs Flasher <a name="4.10.3.4"></a>

Universal Silicon Labs Flasher     https://github.com/NabuCasa/universal-silabs-flasher

Install :
```
$ pip install universal-silabs-flasher
```
Get a .gbl firmware.
Send the boot sequence above.
Flash the MG24 :
```
universal-silabs-flasher --device /dev/ttyUSB1 flash --firmware xxxxx-115200.gbl
```

#### 4.10.3.5 - Firmware update with Silicon Labs Commander <a name="4.10.3.5"></a>
https://siliconlabs.github.io/matter/2.3.0-1.3-alpha.2/general/FLASH_SILABS_DEVICE.html
https://community.silabs.com/s/article/setting-up-raspberry-pi-for-development-with-silicon-labs-emberznet-stack

Install :
```
wget https://www.silabs.com/documents/public/software/SimplicityCommander-Linux.zip
unzip SimplicityCommander-Linux.zip
cd SimplicityCommander-Linux/
tar -xvf Commander_linux_aarch64_1v22p1b1957.tar.bz
cd commander./
```
Simplicity Commander requires that the SEGGER J-Link software pack is installed

Verify:
```
./commander --version
```
Send the boot sequence above.
Check if the communication with the bootloader
```
./commander device info --serialport /dev/ttyUSB1 --baudrate 115200
```
Send the boot sequence above.
Flash an Hex file:
```
./commander flash firmware.hex --serialport /dev/ttyUSB1 --baudrate 115200
```
Flash a bin file:
```
./commander flash firmware.bin --serialport /dev/ttyUSB1 --baudrate 115200 --address 0x08000000
```
Reset and Run the MG24 Firmware:
```
./commander reset --serialport /dev/ttyUSB1
```
### 4.10.4 - Usefull Links <a name="4.10.4"></a>
https://www.silabs.com/support/training/developing-with-matter-on-the-mg24
https://wiki.seeedstudio.com/xiao_mg24_matter/
https://tutoduino.fr/en/tutorials/matter-xiao-mg24/
https://wiki.seeedstudio.com/xiao_mg24_getting_started/
https://community.silabs.com/s/question/0D5Vm00000vUohmKAC/flashing-the-xiao-mg24-sense?language=fr
https://docs.zephyrproject.org/latest/boards/seeed/xiao_mg24/doc/index.html
https://siliconlabs.github.io/matter/2.3.0-1.3-alpha.2/OVERVIEW.html

## 4.11 - LoRa/Sigfox <a name="4.11"></a>
# <code style="color : RED">TBC</code>

## 4.12 - RTC <a name="4.12"></a>

For ML2032 rechargeable battery, add this line to config.txt and reboot :
```
dtparam=rtc_bbat_vchg=3000000
```
Verify charging voltage :
```
cat /sys/class/rtc/rtc0/charging_voltage
cat /sys/class/rtc/rtc0/charging_voltage_max
cat /sys/class/rtc/rtc0/charging_voltage_min
```
Read vbat voltage on the PMIC
```
watch -n 1 vcgencmd pmic_read_adc
```
---
# 5 - TIPS <a name="5"></a>
## 5.1 - Benchmark 💪🏻 <a name="5.1"></a>
Config : Raspberry PI OS Desktop on EMMc + Samsung 64GB USB-C Drive

#### Pi Benchmark script
```
sudo curl https://raw.githubusercontent.com/TheRemote/PiBenchmarks/master/     
```
```
Category                  Test                      Result     
HDParm                    Disk Read                 308.40 MB/sec            
HDParm                    Cached Disk Read          212.31 MB/sec            
DD                        Disk Write                110 MB/s                 
FIO                       4k random read            23621 IOPS (94486 KB/s)  
FIO                       4k random write           25252 IOPS (101011 KB/s) 
IOZone                    4k read                   44281 KB/s               
IOZone                    4k write                  67744 KB/s               
IOZone                    4k random read            44411 KB/s               
IOZone                    4k random write           55907 KB/s               
                          Score: 13083                                       
```
#### GeekBench6
```
cd ~/Downloads
wget https://cdn.geekbench.com/Geekbench-6.4.0-LinuxARMPreview.tar.gz
tar xf Geekbench-6.4.0-LinuxARMPreview.tar.gz
rm Geekbench-6.4.0-LinuxARMPreview.tar.gz
cd Geekbench-6.4.0-LinuxARMPreview
./geekbench6
```
```
890 Single core
1936 Multi-core
```
#### sysbench
```
sudo apt -y install sysbench
sysbench --test=cpu --cpu-max-prime=20000 --num-threads=4 run
```
```
CPU speed:
    events per second:  4036.34
```
## 5.2 - Shrink a pi image  <a name="5.2"></a>
https://github.com/Drewsif/PiShrink
## 5.3 - Manage Energy <a name="5.3"></a>
https://forums.raspberrypi.com/viewtopic.php?t=361542
https://forums.raspberrypi.com/viewtopic.php?t=360658
### Underclocking
100% CPU : 10.4W@2.4Ghz, 8.4W@1.5Ghz, 5W@600Mhz, 4.6W@300Mhz
sudo nano /boot/firmware/config.txt
```
arm_freq=1500
arm_freq_min=600
gpu_freq=400
```
To get the actual clock :
```
vcgencmd measure_clock arm
```
Links :
https://www.jeffgeerling.com/blog/2023/overclocking-and-underclocking-raspberry-pi-5
https://ohyaan.github.io/tips/power_saving_on_raspberry_pi_os__complete_optimization_guide/#display-and-interface-optimizations
### Disable PCIE switch
You can gain more than 1W if you don't need any SSD or TPU M.2 PCIe Module (Cellular used USB).
In Config.txt
```
#--- No PCIe M.2 modules -> Desactivate the PCIe switch (-1.3W)
dtparam=pciex1=off
```
### Reduce Ethernet to 100 MB
https://raspberrypi.stackexchange.com/questions/116677/force-wired-ethernet-speed-to-100-full
ethtool eth0
sudo ethtool -s eth0 advertise 0x008
### Disable Wireless
In config.txt :
```
dtoverlay=disable-wifi
dtoverlay=disable-bt
```
### Disable HDMI
https://lowendbox.com/blog/how-to-turn-off-the-hdmi-monitor-on-your-raspberry-pi-5-its-not-as-easy-as-you-might-think/
https://forums.raspberrypi.com/viewtopic.php?t=374678
https://www.raspberrypi.com/documentation/computers/os.html#vcgencmd
```
vcgencmd display_power 0 7
```
###  Disable audio
In config.txt :
```
#dtparam=audio=on
```
### View cpu-freq governors statistics
https://www.kernel.org/doc/Documentation/cpu-freq/governors.txt
```
cat /sys/devices/system/cpu/cpufreq/policy0/stats/time_in_state
```
### Halt mode with periodic RTC Wake Up
https://raspberrypi.stackexchange.com/questions/147353/can-i-use-raspberry-pi-5-into-low-power-mode-programmatically
https://www.jeffgeerling.com/blog/2023/reducing-raspberry-pi-5s-power-consumption-140x
```
sudo rpi-eeprom-config -e
```
```
[all]
BOOT_UART=1
WAKE_ON_GPIO=0
POWER_OFF_ON_HALT=1

# Default BOOT_ORDER for provisioning
# SD -> NVMe -> USB -> Network
BOOT_ORDER=0xf2461
```
The Halt mode power is 278mW, you can test it with the shutdown command:
```
sudo shutdown now
```
## 5.4 - Watchdog <a name="5.4"></a>
https://diode.io/blog/running-forever-with-the-raspberry-pi-hardware-watchdog

Enable the hardware watchdog and reboot:
```
sudo su
echo 'dtparam=watchdog=on' >> /boot/config.txt
reboot
```
Install the watchdog system service:
```
sudo su
echo 'watchdog-device = /dev/watchdog' >> /etc/watchdog.conf
echo 'watchdog-timeout = 15' >> /etc/watchdog.conf
echo 'max-load-1 = 24' >> /etc/watchdog.conf
```
Enable the service:
```
sudo systemctl enable watchdog
sudo systemctl start watchdog
sudo systemctl status watchdog
```
Now next time your Xplorer freezes, the hardware watchdog will restart it automatically after 15 seconds.

If you want to test this you can try running a fork bomb on your shell:
```
sudo bash -c ':(){ :|:& };:'
```
## 5.5 - NAS Setup <a name="5.5"></a>
The Xplorer can be setup with 2 NVMe SSD to make an embedded RAID NAS.
https://ohyaan.github.io/tips/network_attached_storage__nas__setup_guide/

## 5.6 - Reduce boot time <a name="5.6"></a>
#### Get the boot time
```
$ systemd-analyze
Startup finished in 1.342s (kernel) + 4.842s (userspace) = 6.184s 
graphical.target reached after 4.830s in userspace.
```
#### To reduce boot time
https://ohyaan.github.io/tips/raspberry_pi_boot_time_optimization__complete_performance_guide/#understanding-the-boot-process
## 5.7 - CPU Isolation and Task Affinity for Multicore Optimization <a name="5.7"></a>
https://ohyaan.github.io/tips/cpu_isolation_and_task_affinity_for_multicore_optimization/

## 5.8 - Security Hardening <a name="5.8"></a>
https://ohyaan.github.io/tips/raspberry_pi_security_hardening_complete_guide/#network-security

---
# 6 - GPIO CONFIGURATION <a name="6"></a>
```
pinctrl
```
```
 0: a2    pn | hi // ID_SDA/GPIO0 = TXD1
 1: a2    pu | hi // ID_SCL/GPIO1 = RXD1
 2: ip    pu | hi // GPIO2 = input
 3: ip    pu | hi // GPIO3 = input
 4: a2    pn | hi // GPIO4 = TXD2
 5: a2    pu | hi // GPIO5 = RXD2
 6: no    pu | -- // GPIO6 = none
 7: ip    pu | hi // GPIO7 = input
 8: a2    pn | hi // GPIO8 = TXD3
 9: a2    pu | hi // GPIO9 = RXD3
10: ip    pd | hi // GPIO10 = input
11: op dl pd | lo // GPIO11 = output
12: a2    pn | hi // GPIO12 = TXD4
13: a2    pu | hi // GPIO13 = RXD4
14: a4    pn | hi // GPIO14 = TXD0
15: a4    pu | hi // GPIO15 = RXD0
16: op dh pd | hi // GPIO16 = output
17: op dh pd | hi // GPIO17 = output
18: op dh pd | hi // GPIO18 = output
19: a0    pd | lo // GPIO19 = SPI1_MISO
20: a0    pd | lo // GPIO20 = SPI1_MOSI
21: a0    pd | lo // GPIO21 = SPI1_SCLK
22: a0    pn | lo // GPIO22 = SD0_CLK
23: a0    pu | lo // GPIO23 = SD0_CMD
24: a0    pu | lo // GPIO24 = SD0_DAT0
25: a0    pu | lo // GPIO25 = SD0_DAT1
26: a0    pu | lo // GPIO26 = SD0_DAT2
27: a0    pu | lo // GPIO27 = SD0_DAT3
28: op dh pd | hi // PCIE_PWR_EN/GPIO28 = output
29: no    pu | hi // FAN_TACH/GPIO29 = none
30: no    pu | -- // HOST_SDA/GPIO30 = none
31: no    pu | -- // HOST_SCL/GPIO31 = none
32: op dh pd | hi // ETH_RST_N/GPIO32 = output
33: ip    pu | hi // PCIE_DET_WAKE/GPIO33 = input
34: op dl pd | lo // CD0_IO0_MICCLK/GPIO34 = output
35: ip    pn | hi // CD0_IO0_MICDAT0/GPIO35 = input
36: no    pd | lo // RP1_PCIE_CLKREQ_N/GPIO36 = none
37: ip    pu | hi // ETH_IRQ_N/GPIO37 = input
38: no    pd | hi // SDA0/GPIO38 = none
39: op dh pd | hi // SCL0/GPIO39 = output
40: no    pd | lo // GPIO40 = none
41: no    pd | lo // GPIO41 = none
42: a2    pd | hi // USB_VBUS_EN/GPIO42 = VBUS_EN1
43: a2    pu | hi // GPIO43 = VBUS_OC1
44: op dl pd | lo // RP1_STAT_LED/GPIO44 = output
45: op dh pd | hi // FAN_PWM/GPIO45 = output
46: op dh pd | hi // GPIO46 = output
47: no    pd | lo // 2712_WAKE/GPIO47 = none
48: op dh pd | hi // GPIO48 = output
49: op dh pd | hi // GPIO49 = output
50: no    pd | -- // GPIO50 = none
51: no    pd | -- // GPIO51 = none
52: no    pu | -- // GPIO52 = none
53: no    pu | hi // GPIO53 = none
101: op dh pu | hi // 2712_BOOT_CS_N/GPIO1 = output
102: a7    pn | hi // 2712_BOOT_MISO/GPIO2 = VC_SPI0_MISO
103: a6    pn | hi // 2712_BOOT_MOSI/GPIO3 = VC_SPI0_MOSI
104: a6    pn | lo // 2712_BOOT_SCLK/GPIO4 = VC_SPI0_SCLK
110: ip    pd | lo // GPIO10 = input
111: ip    pd | lo // GPIO11 = input
112: ip    pd | lo // GPIO12 = input
113: ip    pd | lo // GPIO13 = input
114: a1    pd | lo // GPIO14 = SPI_S_MOSI_OR_BSC_S_SDA
115: a1    pd | lo // GPIO15 = SPI_S_SCK_OR_BSC_S_SCL
118: ip    pd | lo // GPIO18 = input
119: ip    pd | lo // GPIO19 = input
120: ip    pu | hi // PWR_GPIO/GPIO20 = input
121: ip    pd | lo // 2712_G21_FS/GPIO21 = input
122: ip    pu | hi // GPIO22 = input
123: ip    pd | lo // GPIO23 = input
124: a4    pn | lo // BT_RTS/GPIO24 = UART_RTS_0
125: a4    pu | lo // BT_CTS/GPIO25 = UART_CTS_0
126: a4    pn | hi // BT_TXD/GPIO26 = UART_TXD_0
127: a4    pu | hi // BT_RXD/GPIO27 = UART_RXD_0
128: op dh pd | hi // WL_ON/GPIO28 = output
129: op dh pd | hi // BT_ON/GPIO29 = output
130: a1    pn | hi // WIFI_SDIO_CLK/GPIO30 = SD2_CLK
131: a1    pu | hi // WIFI_SDIO_CMD/GPIO31 = SD2_CMD
132: a1    pu | hi // WIFI_SDIO_D0/GPIO32 = SD2_DAT0
133: a1    pu | hi // WIFI_SDIO_D1/GPIO33 = SD2_DAT1
134: a1    pu | hi // WIFI_SDIO_D2/GPIO34 = SD2_DAT2
135: a1    pu | hi // WIFI_SDIO_D3/GPIO35 = SD2_DAT3
200: a6    pd | hi // RP1_SDA/AON_GPIO0 = VC_SDA0
201: a7    pd | hi // RP1_SCL/AON_GPIO1 = VC_SCL0
202: op dh pd | hi // RP1_RUN/AON_GPIO2 = output
203: op dl pd | lo // SD_IOVDD_SEL/AON_GPIO3 = output
204: op dh pd | hi // SD_PWR_ON/AON_GPIO4 = output
205: op dl pd | lo // ANT1/AON_GPIO5 = output
206: op dh pd | hi // ANT2/AON_GPIO6 = output
208: ip    pd | lo // 2712_WAKE/AON_GPIO8 = input
209: op dl pd | lo // 2712_STAT_LED/AON_GPIO9 = output
212: ip    pd | lo // PMIC_INT/AON_GPIO12 = input
213: a2    pu | hi // UART_TX_FS/AON_GPIO13 = VC_TXD0
214: a3    pu | hi // UART_RX_FS/AON_GPIO14 = VC_RXD0
232: a1    -- | hi // HDMI0_SCL/AON_SGPIO0 = HDMI_TX0_BSC_SCL
233: a1    -- | hi // HDMI0_SDA/AON_SGPIO1 = HDMI_TX0_BSC_SDA
234: a1    -- | hi // HDMI1_SCL/AON_SGPIO2 = HDMI_TX1_BSC_SCL
235: a1    -- | hi // HDMI1_SDA/AON_SGPIO3 = HDMI_TX1_BSC_SDA
236: a2    -- | hi // PMIC_SCL/AON_SGPIO4 = BSC_M2_SCL
237: a2    -- | hi // PMIC_SDA/AON_SGPIO5 = BSC_M2_SDA
```

---
# 7 - SELF-TEST <a name="7"></a>
#### 1 & 2 - Peripherals detection and COM & CANbus in reception:

```
stty -F /dev/ttyAMA2 speed 115200 cs8 -cstopb -parenb
stty -F /dev/ttyAMA3 speed 115200 cs8 -cstopb -parenb
stty -F /dev/ttyAMA4 speed 115200 cs8 -cstopb -parenb
stty -F /dev/ttyUSB0 speed 115200 cs8 -cstopb -parenb
stty -F /dev/ttyUSB1 speed 115200 cs8 -cstopb -parenb
stty -F /dev/ttyUSB2 speed 115200 cs8 -cstopb -parenb
stty -F /dev/ttyUSB3 speed 115200 cs8 -cstopb -parenb
sudo ip link set can0 up type can bitrate 250000
sudo ip link set can1 up type can bitrate 250000

echo -e "\n1️⃣  Peripherals self-test"
uname -a | grep -q "Debian 1:6.12.47-1+rpt1~bookworm (2025-09-16) aarch64" && echo "✅ Bookworm Headless Detected" || echo "⚠️ Bookworm Headless NOT Detected"
uname -a | grep -q "Debian 1:6.12.62-1+rpt1 (2025-12-18) aarch64" && echo "✅ Trixie Headless Detected" || echo "⚠️ Trixie Headless NOT Detected"
ethtool eth0 | grep -q "Speed: 1000Mb/s" && echo "✅ Ethernet GbE OK" || echo "❌ Ethernet NOT GbE"
sudo i2cdetect -l | grep -q "i2c-13" && echo "✅ I2C OK" || echo "❌ I2C not detected"
ls -l /dev/tpm* | grep -q "/dev/tpm0" && echo "✅ TPM Driver OK" || echo "❌ TPM driver not detected"
tpm2 getcap properties-fixed | grep -q "TPM2_PT_FAMILY_INDICATOR:" && echo "✅ TPM Chip OK" || echo "❌ TPM Chip KO"
dmesg | grep -i -E "(mcp|spi)" | grep -q "mcp251xfd spi1.2 can0: MCP2518FD" && dmesg | grep -i -E "(mcp|spi)" | grep -q "mcp251xfd spi1.1 can1: MCP2518FD" && echo "✅ can0 and can1 detected" || echo "❌ can0 and/or can1 missing"
ifconfig -a | grep -q can0 && ifconfig -a | grep -q can1 && echo "✅ Interfaces can0 and can1 are present" || echo "❌Interfaces can0 and/or can1 are missing"
lsusb | grep -q "FT4232H" && echo "✅ FT4232H detected" || echo "❌ FT4232H NOT detected"
ls /dev/ttyAMA1 | grep -q "/dev/ttyAMA1" && echo "✅ COM1 detected" || echo "❌ COM1 NOT detected"
ls /dev/ttyAMA2 | grep -q "/dev/ttyAMA2" && echo "✅ COM2 detected" || echo "❌ COM2 NOT detected"
ls /dev/ttyAMA3 | grep -q "/dev/ttyAMA3" && echo "✅ COM3 detected" || echo "❌ COM1 NOT detected"
ls /dev/ttyAMA4 | grep -q "/dev/ttyAMA4" && echo "✅ COM4 detected" || echo "❌ COM2 NOT detected"
ls /dev/ttyUSB0 | grep -q "/dev/ttyUSB0" && echo "✅ RXDA detected" || echo "❌ RXDA NOT detected"
ls /dev/ttyUSB1 | grep -q "/dev/ttyUSB1" && echo "✅ RXDB detected" || echo "❌ RXDA NOT detected"
ls /dev/ttyUSB2 | grep -q "/dev/ttyUSB2" && echo "✅ RXDC detected" || echo "❌ RXDA NOT detected"
ls /dev/ttyUSB3 | grep -q "/dev/ttyUSB3" && echo "✅ RXDD detected" || echo "❌ RXDA NOT detected"
lspci | grep -q "ASM1184e" && echo "✅ ASM1184e detected" || echo "❌  ASM1184e  NOT detected"
lspci | grep -q "Samsung" && echo "✅ Samsung SSD module detected" || echo "⚠️  Samsung SSD module NOT detected"
lsblk| grep -q "nvme0n1" && echo "✅ Main SSD mounted" || echo "⚠️  Main SSD NOT mounted"
lsusb | grep -q "EM060K-GL" && echo "✅ 4G LTE module detected" || echo "⚠️  4G LTE module NOT detected"
lsusb | grep -q "Qualcomm / Option SDXBAAGHA-IDP" && echo "✅ 5G RedCap module detected" || echo "⚠️  5G RedCap module NOT detected"
ifconfig | grep -q "usb0:" && echo "✅ Cellular network Detected" || echo "⚠️  Cellular network not Detected"
ping -q -c1 -I usb0 google.com &>/dev/null && echo "✅ Ping Cellular OK" || echo "⚠️  Ping Cellular NOT Working"
lsblk| grep -q "mmcblk2" && echo "✅ uSD mounted" || echo "⚠️  uSD NOT mounted"
lsusb | grep -q "Flash Drive" && echo "✅ External Flash drive detected on USB-C" || echo "⚠️  External Flash drive NOT detected on USB-C"
printf "💾 eMMC: " && lsblk -dn -o SIZE /dev/mmcblk0
printf  "💾 SDRAM: " && grep MemTotal /proc/meminfo
printf  "💾 SSD: " && lsblk -dn -o SIZE /dev/nvme0n1

echo -e "\nPress a key..."
read -n 1 -s
echo -e "\n2️⃣  Test COM ports in Reception at 115200 Bauds and CANbuses in Reception at 250KB, CTRL-C to exit"
cat /dev/ttyAMA1 | sed 's/^/[COM1] /' &
cat /dev/ttyAMA2 | sed 's/^/[COM2] /' &
cat /dev/ttyAMA3 | sed 's/^/[COM3] /' &
cat /dev/ttyAMA4 | sed 's/^/[COM4] /' &
cat /dev/ttyUSB0 | sed 's/^/[RXDA] /' &
cat /dev/ttyUSB1 | sed 's/^/[RXDB] /' &
cat /dev/ttyUSB2 | sed 's/^/[RXDC] /' &
cat /dev/ttyUSB3 | sed 's/^/[RXDD] /' &
candump can1 | sed 's/^/[CAN1] /' &
candump can0 | sed 's/^/[CAN2] /' &
wait
```
#### 3 - Test all the COMs and CANbuses ports in transmit :
Note: COM1 is tested with the RS232 Console
```
echo -e "\n3️⃣  Test COM ports in Transmit at 115200 Bauds and CANbuses Transmit at 250KB"
stty -F /dev/ttyAMA0 speed 115200 cs8 -cstopb -parenb
stty -F /dev/ttyAMA2 speed 115200 cs8 -cstopb -parenb
stty -F /dev/ttyAMA3 speed 115200 cs8 -cstopb -parenb
stty -F /dev/ttyAMA4 speed 115200 cs8 -cstopb -parenb
sudo ip link set can1 up type can bitrate 250000
sudo ip link set can0 up type can bitrate 250000
while true; do
  printf "TX COM2 OK\r\n" | tee /dev/ttyAMA2 > /dev/null
  printf "TX COM3 OK\r\n" | tee /dev/ttyAMA3 > /dev/null
  printf "TX COM4 OK\r\n" | tee /dev/ttyAMA4 > /dev/null
  cansend can1 7DF#0201050000000000
  cansend can0 7DF#0201050000000000 
  sleep 1
done
```

