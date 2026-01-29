# <code style="color : BLACK">XPLORER CM5 FLEX - Datasheet - 🅰🆄🆂🆃🆁🅰🅻 Electronics</code>

www.austral-eng.com - Intelligent Technologies for Marine, Industrial IoT and Unmanned Vehicles

**Xplorer CM5 – Waterproof Rugged Industrial Edge IoT/AIoT Controller & Embedded Mission Computer – Raspberry PI CM5 & Hailo AI Ecosystems**

Xplorer CM5 are a familly of products. They can be used when reliability is not an option for IIoT, AIoT & Edge Gateways or Controllers for Smart, Connected Automation and Supervision but also as Embedded Mission Computers for Sea, Air & Land Intelligent Mobility in harsh environment.

![image](https://github.com/austral-electronics/Xplorer/raw/main/images/Xplorer_CM5_Flex_Overview.png)
## 📚 Table of Contents
- **[PRODUCT HIGHLIGHT](#0)** 
- **[1 - SWAP-C MODULAR DESIGN](#1)** 
- **[2 - TECHNICAL SPECIFICATIONS](#2)** 
- **[3 - ORDERING INFORMATION](#3)**
- **[4 - OPTIONAL ACCESSORIES](#4)**
- **[5 - DIMENSIONS](#5)**
- **[6 - INSTALLATION](#6)**
- **[7 - ELECTRICAL INTERFACES](#7)**
  - [7.1 - CAN1/PWR](#7.1)
  - [7.2 - USB-C](#7.2)
  - [7.3 - DAQ/CAN2](#7.3)
  - [7.4 - SERIALS](#7.4)
  - [7.5 - LAN](#7.5)
  - [7.6 - WIFI/BT](#7.6)
  - [7.7 - LPWAN/LTE2/SAT2](#7.7)
  - [7.8 - GNSS](#7.8)
  - [7.9 - LTE1/SAT1](#7.9)
  - [7.10 - Right cap : BOOT @ uSD-CARD](#7.10)
  - [7.11 - Left cap : Micro HDMI & nano SIM card](#7.11)
- **[8 - OPTIONAL MODULES](#8)**
  - [8.1 - SSD](#8.1)
  - [8.2 - 4G LTE-A](#8.2)
  - [8.3 - 5G RedCap](#8.3)
  - [8.4 - AI Accelerator](#8.4)
  - [8.5 - GNSS RTK+IMU](#8.5)
  - [8.6 - Multi-Protocol Wireless Network co-processor](#8.5)
  - [8.7 - LoRa/SigFox](#8.5)
- **[9 - MAINTENANCE](#9)**
  - [9.1 - Change the RTC battery](#9.1)
  - [9.2 - Change an SSD](#9.2)
  - [9.3 - Repair a board](#9.3)
- **[10 - SOFTWARE SUPPORT](#10)**
- **[11 - CONTACT](#11)**
    
---
## PRODUCT HIGHLIGHT <a name="0"></a>
✅ **Raspberry PI CM5** based waterproof rugged industrial edge IoT/AIoT gateway, embedded mission computer, In-vehicle/Boat Smart Hub, Roadside computer…  
✅ Ecosystem with a **huge community** facilitating support, scalability, and updates  
✅  **Future Proof** and **Highly customizable** modular design   
✅  **Best in class wireless connectivity capability** (WiFi, BT, BLE, GNSS, 4G LTE, 5G, Direct-To-Cell Ready, NB-IoT NTN Ready, LoRa, SigFox, Matter, Thread, Zigbee...)  
✅  Optional **Hailo AI Accelerator** providing up to 2x 26 TOPS of AI for machine learning, video analytics, smart automation and supervision  
✅  **Rich in connectivity** and industrial field buses (1x GbE, 8x Serials, 2x CANbus, DAQ)  
✅  **Numerous storage** solutions (eMMC, Multiples M.2 SSD, uSD card, USB-C drive)  
✅  **Cybersecurity** (TPM2.0, AES256 SSD option, Unique ID, security uSD…)  
✅  **B2B Ready** : customize configuration, markings and packaging  

## 1 - SWAP-C MODULAR DESIGN <a name="1"></a>
![image](https://github.com/austral-electronics/Xplorer/raw/main/images/Xplorer_CM5_Flex_Inside.png)

---
## 2 - TECHNICAL SPECIFICATIONS <a name="2"></a>
![image](https://github.com/austral-electronics/Xplorer/raw/main/images/Xplorer_CM5_Flex_Spec_1_2.png)
![image](https://github.com/austral-electronics/Xplorer/raw/main/images/Xplorer_CM5_Flex_Spec_2_2.png)

---
## 3 - ORDERING INFORMATION <a name="3"></a>

**Build your part number :** In this example P/N 200-003-002(3.1)-W-8-32-256-N-5GS-Y-C-B

![image](https://github.com/austral-electronics/Xplorer/raw/main/images/Xplorer_CM5_Flex_Ordering.png)

---

## 4 - OPTIONAL ACCESSORIES <a name="4"></a>
![image](https://github.com/austral-electronics/Xplorer/raw/main/images/Xplorer_CM5_Flex_Accessories.png)

All cables and antennas are standard and available for purchase off the shelf for reasonable prices.

---

## 5 - DIMENSIONS <a name="5"></a>
![image](https://github.com/austral-electronics/Xplorer/raw/main/images/Xplorer_CM5_Flex_Dimensions.png)
---

## 6 - INSTALLATION <a name="6"></a>

The Xplorer CM5 is thermally designed to be installed vertically with the M12 connectors facing downwards and the SMA connectors facing upwards.  
By default, the mounting is wall-mounted, but DIN rail mounting is available as an option.  
If you do not wish to drill holes, you can attach the product using two strips of 3M Dual Lock after thoroughly degreasing the surfaces.  
We can also supply carbon supports with inserts to be bonded with epoxy glue.  

⚠️ In an exposed environment, put caps on unused connectors.

## 7 - ELECTRICAL INTERFACES <a name="7"></a>
### 7.1 - CAN1/PWR <a name="7.1"></a>
This connector is compatible with the standardised DeviceNet/NMEA2000 5-pin male⁉️ A-coded M12 screw connector.  
It allows both the Xplorer CM5 to be powered and communication via a CANbus or a CAN-FD bus.  
If you are connecting the Xplorer CM5 directly to an NMEA2000 bus, place it close to the power supply T in order to minimise voltage drops.  
| Pin  | Name            | Reference | N2K cable | Description                                                                          
|----------------------- |-----------|-----------|-------------|-|
| J17.1| **CAN1-SHIELD** | GND       | Shield    | CAN1 Shield
| J17.2| **VIN**         | GND       | Red       | 8-33V / Power Supply Input Positive
| J17.3| **GND**         | GND       | Black     | 0V / Power Supply Input Negative
| J17.4| **CAN1-H**      | GND       | White     | CAN1 Positive/NET-H (To N2K White wire) 
| J17.5| **CAN1-L**      | GND       | Blue      | CAN1 Negative/NET-L (To N2K Blue wire)
 
CAN-FD Specifications:
- Uses the Microchip [MCP2518FDT](https://ww1.microchip.com/downloads/aemDocuments/documents/OTH/ProductDocuments/DataSheets/External-CAN-FD-Controller-with-SPI-Interface-DS20006027B.pdf) controller connected to SPI1.1
- 3kV Isolation, 5 Mbps Max, ESD +/-8kV, +/-58V DC bus fault protection, +/-12V common-mode voltage range

### 7.2 - USB-C <a name="7.2"></a>
This connector has a dual role :
- It allows a Linux image to be bootloaded into the EMMc if the bootload switch is set to the SMA connectors side (top) when the power is turned on. The blue Status LED lights up continuously in this mode.
- Otherwise, it is a USB-C connector that delivers both USB 2.0 (480Mbits/s half duplex) and USB 3.0 (5 Gbits/s full duplex), and is dual role, i.e. it can be either a host or a device. In host mode, it can power a device with 5V up to 1A, you can connect peripherals such as flash drive, 5GbE Ethernet, camera, voice interface, external DAQ, more Serials, more CANbus etc.

**Note :**
- ⚠️ This connector is not compatible with DisplayPort (DP Alt Mode), there is a Micro HDMI connector under a plug for connecting a monitor for a development need.
- 💻 For development, it is also possible to connect one or more monitors, keyboard, mouse, webcam via a **USB-C DisplayLink docking station**. Latency will be much lower than with a Remote Desktop solution via GbE ou WiFi. You will need to choose a docking station with its own power supply so as not to place too much thermal stress on the Xplorer CM5.
- 💧 This connector is waterproof but not dustproof. It is best to put a silicone plug on it when not in use, you can also add vaseline to protect more from corrosion.
- 🔨 USB-C is not an industrial connector, for environments subject to shocks and vibrations, a single-screw locking mechanism solution compliant with the Universal Serial Bus Type-C [specification](https://www.usb.org/sites/default/files/documents/usb_type-c_locking_connector_specification_rev_1_0_20160309_0.pdf) can be provided as an enclosure option.

**Recommended USB-C peripherals:**
- Flash Drive: [Samsung MUF 64DA](https://www.samsung.com/fr/memory-storage/usb-flash-drive/usb-flash-drivetype-c-64gb-muf-64da-apc/) familly (64 to 512GB) 
- External Hailo-10H AI Accelerator: [ASUS UGen300](https://www.asus.com/motherboards-components/ai-accelerator/ugen/ugen300-usb-8g/)

### 7.3 - DAQ/CAN2 <a name="7.3"></a>
This connector is a 12-pin male A-coded M12 screw type.
It allows data aquisition and more field connectivity:
- ✅ **2x Open Drain Digital Output**
    - <27V <1A (6A peak), 27V/350W ESD Protection Diode, 30kV ESD.
- ✅ **2x 12 bits 0-2.5V or 0-5V Analog Output**
    -  Up to 400 kSPS, 13.5V/150W ESD Protection Diode, +/- 15kV ESD
    -  ⚠️ 2K output impedance (to ensure robustness against wiring errors and ESD)
    -  👍 Can also be used as general-purpose digital input/output pins.
    -  🧩 Optional RC filter (C154, C153 not implanted by default)
- ✅ **Up to 4x 12 bits 0-2.5V or 0-5V Analog Input**
    -  Up to 400 kSPS, 3.5V/150W ESD Protection Diode, +/- 15kV ESD, 13.3K/10nF RC Filter
    -  ⚠️ Share with 4x RS232 inputs (Rx Only)
    -  👍 Can also be used as general-purpose digital input/output pins.
    -  🧩 Other RC Filter in hardware option
- ✅ **Up to 4x RS232 inputs (Rx Only mode)**
    -  14V/150W ESD Diode, 3.3K input impedance below 0V or above 5V.
    -  ⚠️ Shared with 4x Analog inputs
    -  ⚠️ IN1_RXDB is not functional with the **Matter** hardware option
- ✅ **1x isolated CANbus or CAN-FD**
    - 3kV Isolation, 5 Mbps Max, ESD +/-8kV, +/-58V DC bus fault protection, +/-12V common-mode voltage range.
    - It uses the Microchip [MCP2518FDT](https://ww1.microchip.com/downloads/aemDocuments/documents/OTH/ProductDocuments/DataSheets/External-CAN-FD-Controller-with-SPI-Interface-DS20006027B.pdf) CAN-FD controller connected to SPI1.2

The **DAQ** uses the chip Analog Device [AD5592R](https://www.analog.com/media/en/technical-documentation/data-sheets/ad5592r.pdf), a 8-Channel (IO1 to IO7), 12-Bit, configurable ADC/DAC/GPIO with On-Chip 20 ppm/°C reference and a SPI interface connected to the SPI1.0.  
It has a total throughput rate of 400 kSPS and an integrated temperature indicator.

| CON  | PCB| Name        | Reference | Color    | IO | Description                                                                          
|------|----|-------------|-----------|----------|----|-|
| J5.1 |  2 | **OUT4**    | GND_ANA   | Brown    |IO7| Open Drain digital Output 4
| J5.2 |  1 | **GND_CAN2**| -         | Blue     | - | Isolated CAN2 Ground
| J5.3 |  9 | **CAN2_L**  | GND_CAN2  | White    | - | Isolated CAN2-L (To N2K Blue wire)
| J5.4 |  8 | **CAN2_H**  | GND_CAN2  | Green    | - | Isolated CAN2-H (To N2K White wire)
| J5.5 |  7 | **IN4_RXDC**| GND_ANA   | Pink     |IO3| 12 bits 0-2.5V or 0-5V Analog/Digital Input 4 or RXDC RS232 Rx Only
| J5.6 |  6 | **IN2_RXDA**| GND_ANA   | Yellow   |IO1| 12 bits 0-2.5V or 0-5V Analog/Digital Input 2 or RXDA RS232 Rx Only
| J5.7 |  5 | **IN1_RXDB**| GND_ANA   | Black    |IO0| 12 bits 0-2.5V or 0-5V Analog/Digital Input 1 or RXDB RS232 Rx Only)
| J5.8 |  4 | **OUT2**    | GND_ANA   | Grey     |IO5| 12 bits 0-2.5V or 0-5V Analog/Digital Output
| J5.9 |  3 | **OUT3**    | GND_ANA   | Red      |IO6| Open Drain digital Output 3 (Connected to IO6)
| J5.10| 10 | **GND_ANA** | -         | Violet   | - | Analog Ground (Ground Plane connected to GND via a 0 ohm resistor)
| J5.11| 12 | **IN3_RXDD**| GND_ANA   | Grey/Pink|IO2| 12 bits 0-2.5V or 0-5V Analog/Digital Input 3 or RXDD RS232 Rx Only
| J5.12| 11 | **OUT1**    | GND_ANA   | Red/Blue |IO4| 12 bits 0-2.5V or 0-5V Analog/Digital Output

**Recommanded M12 to wires cable** : Altech [CBF12-S12N0 Familly](https://legacy.altechcorp.com/sensor-connectors/pdfs/Molded_Female_Cable_Assemblies.pdf) ([1m](https://docs.rs-online.com/9161/A700000007160909.pdf), [2m](https://katlax.s3.ap-south-1.amazonaws.com/datasheets/02-M12/A-Coded/MouldedConnector/CBF12-S12N0-02BPUR.pdf) or 5m, PVC or PUR).

### 7.4 - SERIALS <a name="7.4"></a>
This connector is a 12-pin female A-coded M12 screw type.
It allows field connectivity:
- ✅ **COM1 : RS232**
    - Non Isolated, 250Kbps max, +/-15kV ESD
- ✅ **COM2 : RS232 with CTS/PPS Input**
    - Port suitable for GNSS or INS/GNSS with PPS connected to CTS
    - Non Isolated, 250Kbps max, +/-15kV ESD
    - 🧩 The logic level of the PPS can be inverted (hardware option, Implantation of R46 = 0 Ohm)
- ✅ **COM3 : Isolated RS232/RS485/Modbus**
    - 3KVrms Isolation, +/-15kV ESD
    - Set GPIO18 to switch in RS485/Modbus Mode
    - In RS485/Modbus mode : 20Mbps max, No bias or terminator resistor, RTS controls the low impedance, 1/8th Unit Load, up to 256 receivers on bus.
    - In RS232 mode : 1Mbps max
- ✅ **COM4 : Isolated RS485/Modbus**
    - [MAX22025AWA+](https://www.analog.com/media/en/technical-documentation/data-sheets/MAX22025-MAX22028F.pdf) chipset with autoDirection Control (No need impedance control with RTS), 500Kbps max, 3.5kVrms Isolation, +/-10kV ESD.
    - Integrated R6 & R11, 620 ohm bias resistors (To isolated 0V and 5V)
    - ⚠️ 120 ohm terminator not integrated
    - 🧩 16Mbps in hardware option

| Pin   | Name            | Reference| Color    | Description                                                                          
|-------------------------|----------|----------|-------------|-|
| J12.1 | **COM1_RXD**   | GND      | White    | COM1 RS232-RXD
| J12.2 | **COM2_CTS/PPS**| GND      | Brown    | COM2 RS232-CTS (External GNSS PPS Input)
| J12.3 | **COM3_TXD/B**  | GND_SER  | Green    | COM3 Isolated RS232-TXD OR RS485-B or Negative
| J12.4 | **COM3_RTS/A**  | GND_SER  | Yellow   | COM3 Isolated RS232-RTS OR RS485-A or Positive
| J12.5 | **GND_SER**     | -        | Grey     | 0V for isolated ports
| J12.6 | **COM4_A**      | GND_SER  | Pink     | COM4 Isolated RS485-A/P
| J12.7 | **COM4_B**      | GND_SER  | Blue     | COM4 Isolated RS485-B/N
| J12.8 | **COM1_TXD**    | GND      | Red      | COM1 RS232-TXD
| J12.9 | **COM2_TXD**    | GND      | Black    | COM2 RS232-TXD (External GNSS/INS)
| J12.10| **COM2_RXD**    | GND      | Violet   | COM2 RS232-RXD (External GNSS/INS)
| J12.11| **COM3_RXD**    | GND_SER  | Grey/Pink| COM3 Isolated RS232-RXD
| J12.12| **GND**         | -        | Red/Blue | 0V for non isolated ports

**Recommanded Push Pull M12 to wires cable** : Amphenol LTW [M12A-12BMMM-PL8D01](https://mm.digikey.com/Volume0/opasdata/d220001/medias/docus/5849/M12A-XXBMMM-PL8DXX%28E%29.pdf) (1m, PVC with 2m, 3m, 4m or 5m available)

If you need to test the serials or your software with a computer, you will require additional converter and DB9 connectors:

**FTDI USB 2.0 to RS232 cable :**
The M12 **"Serial"** cable is connected to a DB9 Female with the pinout
| Pin| Name| Description                                                                          
|----------------|-------------|-|
| 2  | **RXD_PC**| Connect to COMx_TXD
| 3  | **TXD_PC**| Connect to COMx_RXD
| 5  | **GND**   | Ground 

**[Dtech](https://www.dtechelectronics.com/uploadfile/downloads/IOT5081%20USB%20to%20RS485%20RS422%20Manual.pdf) USB 2.0 to RS485 cable :**
The M12 **"Serial"** cable is connected to a DB9 Female in Half Duplex
mode with the pinout
| Pin| Name         | Description                                                                          
|-------------------|-------------|-|
| 1  | **RS485(A+)**| Connect to COMx_A
| 2  | **RS485(B-)**| Connect to COMx_B
| 5  | **GND**      | Ground 

### 7.5 - LAN <a name="7.5"></a>
This connector is a 8-pin female X-coded M12 screw type.
   
| Pin       | Name      | Color                                                                               
|-----------|-----------|-|
| J13.1     | **BI-DA+**| White/Orange
| J13.2     | **BI-DA-**| Orange
| J13.3     | **BI-DB+**| White/Green
| J13.4     | **BI-DB-**| Green
| J13.5     | **BI-DD+**| White/Brown
| J13.6     | **BI-DD-**| Brown
| J13.7     | **BI-DC-**| White/Blue
| J13.8     | **BI-DC+**| Blue
| J13.Shield| **Shield**| Shield

M12 to RJ45 Cable : 
- [Delock 80868](https://www.delock.com/produkt/87845/merkmale.html?d=557), 1 to 5m
- [Molex 1203410502](https://www.molex.com/content/dam/molex/molex-dot-com/products/automated/en-us/salesdrawingpdf/120/120341/1203410502_sd.pdf)
- [Phoenix contact 1407472](https://eu.mouser.com/datasheet/3/507/7/phoenix_contact_1407472_en.pdf)
- [Eaton NM12-602-05M-BL](https://assets.tripplite.com/product-pdfs/en/nm1260202mbl.pdf)
- [TE RPC-M12X-8MS-1.0SH-RJ45-8MS-TPE](https://www.te.com/en/product-CAT-SI113-M1ZB.html), 1 to 15m
- [CAZN M12-8A1-X-P/S-RJ45-XM](https://www.caznelectrics.com/portfolio/items/m12-rj45-ethernet-industrial-camara-connector)


### 7.6 - WIFI/BT <a name="7.6"></a>
Internally connected to the Wifi/Bluetooth of the RPI CM5.  
Connected to an external SMA(M) 2.4/5Ghz Antenna.  
Antenna included with the antennas starter kit: [Taoglas GW.26.0111](https://cdn.taoglas.com/datasheets/GW.26.0111.pdf) (2.4Ghz, IP65, 2.2dBi Peak).   
Recommanded All-in-One antenna : [Poynting A-PUCK-0005-V2-01](https://poynting.tech/fr/antennas/puck-5/)

### 7.7 - LPWAN/LTE2/SAT2 <a name="7.7"></a>
Internally connected to :
- A Multiprotocol Wireless Module (Matter over Thread, Zigbee, BLE Mesh...)
- Or a LoRa/Sigfox module
- Or the diversity output of a 4G LTE or 5G RedCap M.2 Module

For SMA(M) Antennas.  
Antenna included with the Multiprotocol Wireless starter kit: [Taoglas GW.26.0111](https://cdn.taoglas.com/datasheets/GW.26.0111.pdf) (2.4Ghz, IP65, 2.2dBi).  
Recommanded All-in-One antenna : [Poynting A-PUCK-0005-V2-01](https://poynting.tech/fr/antennas/puck-5/)

### 7.8 - GNSS <a name="7.8"></a>
Internally connected to the 4G LTE or 5G RedCap or GNSS M.2 Module.
For SMA(M) Antennas or cable.
Antenna included with the antennas starter kit: [Quectel YEGT002AA](https://mm.digikey.com/Volume0/opasdata/d220001/medias/docus/5871/Quectel_Antenna_YEGT002AA_Datasheet_V1.2.pdf) (GNSS L1 band, IP64, 1.75dBi)
Recommanded All-in-One antenna : [Poynting A-PUCK-0005-V2-01](https://poynting.tech/fr/antennas/puck-5/)

### 7.9 - LTE1/SAT1 <a name="7.9"></a>
Internally connected to the 4G LTE or 5G RedCap M.2 Module.
For SMA(M) Antennas or cable.
Antenna included with the antennas starter kit: [Pulse/Yaego W1696-M](https://yageogroup.com/content/datasheet/asset/file/DATASHEET_W1696_W1697_W1696-M_W1696-MW) (617MHz ~ 960MHz, 1.71GHz ~ 2.69GHz, 3.4GHz ~ 3.8GHz, IP65 , Gain : -0.5dBi, 1dBi, 0dBi).  
Recommanded All-in-One antenna : [Poynting A-PUCK-0005-V2-01](https://poynting.tech/fr/antennas/puck-5/)

### 7.10 - Right cap : BOOT @ uSD-CARD <a name="7.10"></a>
- Provides access to a boot switch to launch the bootloader via USB-C. The board is in bootloader mode when it is switched toward the SMA connectors.  
- Also allows you to insert a micro SD card for storage or cybersecurity (Push Pull connector). 
> [!CAUTION]
> It is possible to insert the SD card next to the holder and lose it inside the enclosure. The card is inserted using small pliers, with the power turned off and easy access so you can see what you are doing.
> The cap must be lightly greased with vaseline after each opening to ensure a good seal.  
### 7.11 - Left cap : Micro HDMI & nano SIM card <a name="7.11"></a>
- Provides access to a Micro HDMI for debug purpose
- Also allows you to insert a nano SIM card or a 4FF Plastic eSIM card (Push Pull connector)
> [!CAUTION]
> It is possible to insert the SD card next to the connector and lose it inside the enclosure. The card is inserted using small pliers, with the power turned off and easy access so you can see what you are doing.
> The Micro HDMI connector is fragile and not designed for harsh environments. Use it only for debugging in a protected environment.
> The cap must be lightly greased with vaseline after each opening to ensure a good seal. 

Micro HDMI Pinout:
| Pin   | Name                                                                               
|-------|-|
| J16.1 | **Hot Plug Detect/HEC-**
| J16.2 | **Utility/HEAC+**
| J16.3 | **TDMS Data 2+**
| J16.4 | **TDMS Data 2 Shield**
| J16.5 | **TDMS Data 2-**
| J16.6 | **TDMS Data 1+**
| J16.7 | **TDMS Data 1 Shield**
| J16.8 | **TDMS Data 1-**
| J16.9 | **TDMS Data 0+**
| J16.10| **TDMS Data 0 Shield**
| J16.11| **TDMS Data 0-**
| J16.12| **TDMS Clock+**
| J16.13| **TDMS Clock Shield**
| J16.14| **TDMS Clock-**
| J16.15| **CEC (Control)**
| J16.16| **DDC/CEC/HEAC Ground**
| J16.17| **SCL (DDC clock)**
| J16.18| **SDA (DDC data)**
| J16.19| **+5 V Power (power EDID/DDC)**

---
## 8 - OPTIONAL MODULES <a name="8"></a>
### 8.1 - SSD <a name="8.1"></a>
The RPI CM5 module includes an eMMC with up to 64GB of storage that can be configured as read-only to ensure that the OS is not corrupted. An additional SSD is recommended for storing data logs.  

The main SSD is a M.2 key M 2230 NVMe SSD (Up to 2TB in 2025).  
The secondary SSD is a M.2 key M 2230 or 2242 NVMe SSD (Up to 4TB in 2025).  
SSDs can be configured in RAID 0 or 1 to create a robust NAS.  
SSDs can be industrial grade and/or feature an AES256 encryption (contact us).

By default, the SSDs installed are:
- Up to 512GB: [Samsung PM991a](https://github.com/austral-electronics/Xplorer/blob/main/datasheets/SSD/256GB/Samsung%20PM991a-M.2-22x30-SSD-Datasheet_-v0.1_for-Gen_.pdf) 
- From 1TB: [Crucial P310](https://github.com/austral-electronics/Xplorer/blob/main/datasheets/SSD/1TB/crucial-P310-2230-b2c-product-flyer-en_combination.pdf)

### 8.2 - 4G LTE-A <a name="8.2"></a>
The 4G LTE-A functionality is provided by an M.2 key B 3042 module.
The default model installed is the [Quectel EM60K-GL](https://www.quectel.com/product/lte-a-em060k-series/#summary).  
| Item   | Description                                                                               
|-------|-|
| Technology | LTE - cat 6
| Region | Global
| Fallback | 3G 
| Max DL Speed | 300 Mbps
| Max UL Speed | 50 Mbps
| Temperature | -25 - +75 °C
| LTE Bands | B1, B2, B3, B4, B5, B7, B8, B12, B13, B14, B17, B18, B19, B20, B25, B26, B28, B29, B30, B32, B34, B38, B39, B40, B41, B42, B43, B46, B48, B66, B71
| GNSS | GPS, Galileo, GLONASS, BDS, QZSS
| Chipset | Qualcomm SDX12

The documentation is available [here](https://github.com/austral-electronics/Xplorer/tree/main/datasheets/Cellular_DTC/EM060K)

### 8.3 - 5G RedCap <a name="8.3"></a>

The 5G RedCap functionality is provided by an M.2 key B 3042 module.
The default model installed is the [SIMCOM SIM8230G-M2](https://www.simcom.com/product/SIM8230G-M2.html).
This model is low power and compatible with the n25 and n26 bands that will be used for Starlink and AST Mobile **Direct-To-Cell**.

| Item   | Description                                                                               
|-------|-|
| Technology | 5G sub-6, 3GPP Rel-17 RedCap, 1T2R/1T1R operation
| Region | Global
| Fallback | 4G LTE 
| Max DL Speed | 220 Mbps
| Max UL Speed | 100 Mbps
| Temperature | -30 - +70 °C
| 5G Bands | n1, n2, n3, n5, n7, n8, n12, n13, n14, n18, n20, n25, n26, n28, n30, n38, n40, n41, n48, n66, n70, n71, n77, n78, n79 
| LTE Bands | B1, B2, B3, B4, B5, B7, B8, B12, B13, B14, B17, B18, B19, B20, B25, B26, B28, B30, B34, B38, B39, B40, B41, B42, B43, B48, B66, B71
| GNSS | GPS, Galileo, GLONASS, BeiDou
| Chipset | Qualcomm SDX35

The documentation is available [here](https://github.com/austral-electronics/Xplorer/tree/main/datasheets/Cellular_DTC/SIM8230G-M2)

### 8.4 - AI Accelerator <a name="8.4"></a>
### 8.5 - GNSS RTK+IMU <a name="8.5"></a>
### 8.6 - Multi-Protocol Wireless Network co-processor <a name="8.5"></a>
### 8.7 - LoRa/SigFox <a name="8.5"></a>

## 9 - MAINTENANCE <a name="9"></a>

### 9.1 - Change the RTC battery <a name="9.1"></a>

This product include a ML2032 rechargeable battery (lithium manganese dioxide, 3V3, 64mAh) in order to maintain the Real Time Clock and datalog at startup with the correct time without waiting an NTP or GNSS time syncronisation.
> [!CAUTION]
> Change the battery every 10 years. Contact the after sale.

### 9.2 - Change an SSD <a name="9.2"></a>

When performing continuous data logging, for example for video, the SSDs are components that wear out and must be replaced periodically.  
This replacement interval must be calculated based on the characteristics of the SSDs (Size, TBW), the frequency of writes, and the RAID mode.
   
#### Removing the board to acces to the SSD under the board
> [!CAUTION]
> SMA cable must be disconnected and reconnected carefully.
> The thermal pads must be replaced during reassembly.
> Threadlocker must be used on internal screws.
> Contact the after sale. 
#### Close the enclosure
> [!CAUTION]
> The Butyle sealant must be cleaned and replaced after each opening to ensure a good seal.
> Tef-gel must be used between the stainless steel screws and the aluminium enclosure to limit corrosion.
> Contact the after sale.    

---
## 9.3 - Repair a board <a name="9.3"></a>

> [!TIP]
> If you wish to repair a faulty card yourself that is no longer under warranty, here is some useful information.
> The board contains 0201 SMD components, which cannot be changed manually.
> We can take care of the repair or replacement of a component or of a board. Contact the after sale.
### Fuses
| Fuses      | Package | Description|                                                                                                  
|------------|-----|------------|
| **F1**     | 2920 | 30VDC, 4A, 4s Resettable Fuse 
| **F2, F5** | 0603 | 32VDC, 3A Fuse                                                     
---
## 10 - SOFTWARE SUPPORT <a name="10"></a>

Product web page : 	https://austral-eng.com/en/xplorer-cm5/  
Online Software Wiki : 	https://github.com/austral-electronics/Xplorer

---
## 11 - CONTACT <a name="11"></a>

This product can be sold by unit for evaluation or in volume and is designed to fit to your needs (memories, wireless, AI, accessories…).  
It can be customized with your company's visual for 100 units (logo, colors, marking...).  
Austral electronics is a design office, we can support you on your specific needs in electronics, embedded computing, specific Linux, sector specific certification...

**Contact us to begin the pricing and ordering process**

**AUSTRAL ELECTRONICS**  
Espace Teknica, 4 Rue Galilée  
Parc Technologique de Soye  
56270 Ploemeur – FRANCE  

**Mail :** contact@austral-eng.com  
**Website :** http://austral-eng.com/en
