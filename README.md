# wiced_btsdk

This repo is provided for backward compatibility when using BTSDK 2.7.1 or prior. It is provided as a means to update BT chip firmware and APIs. It is not used for applications based on BTSDK 2.8 and above. It contains all available BSPs, chip support libraries, and middleware libraries. It is recommended that all applications update to BTSDK 2.8 and the ModusToolbox 2.2 "MTB" flow model using shared resources dynamically retrieved as needed.

## Folder structure
If using BTSDK code examples released prior to BTSDK 2.8, they require the  'wiced\_btsdk' repo to build and test the apps. 'wiced\_btsdk' includes the 'dev-kit' and 'tools' folders:

**dev-kit**

This folder contains the files that are needed to build the embedded BT apps.

* baselib: Files for chips supported by BTSDK. For example CYW20819, CYW20719, CYW20706, etc.

* bsp: Files for BSPs (platforms) supported by BTSDK. For example CYW920819EVB-02, CYW920721B2EVK-02, CYW920706WCDEVAL etc.

* btsdk-include: Common header files needed by all apps and libraries.

* btsdk-tools: Build tools needed by BTSDK.

* libraries: Profile libraries used by BTSDK apps such as audio, BLE, HID, etc.

**tools**

This folder contains tools and utilities need to test the embedded BT apps.

* btsdk-host-apps-bt-ble: Host apps (Client Control) for BLE and BR/EDR embedded apps, demonstrates use of WICED HCI protocol to control embedded apps.

* btsdk-host-peer-apps-mesh: Host apps (Client Control) and Peer apps for embedded Mesh apps, demonstrates the use of WICED HCI protocol to control embedded apps, and configuration and provisioning from peer devices.

* btsdk-peer-apps-ble: Peer apps for embedded BLE apps.

* btsdk-peer-apps-ota: Peer apps for embedded apps that support Over The Air Firmware Upgrade.

* btsdk-utils: Utilities used in BTSDK such as BTSpy, wmbt, and ecdsa256.

See README.md in the sub folders for more information.



**Using command line**
1. Install ModusToolbox 2.1 or 2.2.

2. On Windows, use Cygwin from \ModusToolbox\tools\_2.x\modus-shell\Cygwin.bat to build apps.
3. git clone 'wiced\_btsdk' repo first. As mentioned earlier, this project contains the SDK used by all apps. You will need to create this project just once in the working directory. For example:<br/>
   > git clone https://github.com/cypresssemiconductorco/wiced_btsdk
4. git clone the BTSDK app repo [ mtb-examples-(board)-btsdk-(type) ]. The application repo directory should be at the same folder level as 'wiced_btsdk'. For example:<br/>
   > git clone https://github.com/cypresssemiconductorco/mtb-examples-CYW920819EVB-02-btsdk-hid
5. The 'wiced\_btsdk' repo contains references to other repos. To download all the required collateral, cd to root folder and use 'make getlibs'. For example:<br/>
   > cd wiced_btsdk<br/>
   > make getlibs<br/>
6. To build the app call make build. For example:<br/>
   > cd ../mtb-examples-CYW920819EVB-02-btsdk-hid<br/>
   > cd hid/ble_mouse/<br/>
   > make build<br/>
7. To program (download to) the board, call:<br/>
   > make qprogram<br/>
8. To build and program (download to) the board, call:<br/>
   > make program<br/>

   Note: make program = make build + make qprogram

## ModusToolbox Tools

Tools installed by ModusToolbox installer:

- Device Configurator:
      Tool to create custom pin mapping for your device.
- Bluetooth Configurator:
      Create and configure BLE GATT Database and BR/EDR SDP records for your application.

## SDK software features

- Dual mode Bluetooth stack included in the ROM (BR/EDR and BLE).
- BT stack and profile level APIs for embedded BT application development.
- WICED HCI protocol to simplify host/MCU application development.
- APIs and drivers to access on-board peripherals
- Bluetooth protocols include GAP, GATT, SMP, RFCOMM, SDP, AVDT/AVCT, BLE Mesh
- BLE and BR/EDR profile APIs, libraries and sample apps
- Support for Over-The-Air (OTA) upgrade.
- Device Configurator for creating custom pin mapping.
- Bluetooth Configurator for creating BLE GATT Database.
- Peer apps based on Android, iOS, Windows, etc. for testing and reference.
- Utilities for protocol tracing, manufacturing testing, etc.
- Documentation for APIs, datasheet, profiles and features.
- BR/EDR profiles: A2DP, AVRCP, HFP, HSP, HID, SPP, MAP, PBAP, OPP
- BLE profiles: Mesh profiles, HOGP, ANP, BAP, HRP, FMP, IAS, ESP, LE COC
- Apple support: Apple Media Service (AMS), Apple Notification Center Service (ANCS), iBeacon, Homekit, iAP2
- Google support: Google Fast Pair Service (GFPS), Eddystone
- Amazon support: Alexa Mobile Accessories (AMA)

## List of boards available for use with BTSDK

- CYW20819A1 chip: CYW920819EVB-02, CYBT-213043-MESH, CYBT-213043-EVAL, CYW920819REF-KB-01
- CYW20820A1 chip: CYW920820EVB-02, CYW989820EVB-01
- CYW20721B2 chip: CYW920721B2EVK-02, CYW920721B2EVK-03, CYW920721M2EVK-02, CYBT-423060-EVAL, CYBT-483062-EVAL, CYBT-413061-EVAL
- CYW20719B2 chip: CYW920719B2Q40EVB-01, CYBT-423054-EVAL, CYBT-413055-EVAL, CYBT-483056-EVAL
- CYW20706A2 chip: CYW920706WCDEVAL, CYBT-353027-EVAL, CYBT-343026-EVAL
- CYW20735B1 chip: CYW920735Q60EVB-01
- CYW20835B1 chip: CYW920835REF-RCU-01
- CYW43012C0 chip: CYW9M2BASE-43012BT, CYW9M2BASE-43012BT20

## Application settings

Application settings below can be configured via makefile of the application or passed in via command line. Options below are available for all applications. Other application specific options might also be available and are documented in the read_me.txt for those applications.

- BT\_DEVICE\_ADDRESS<br/>
    - Set the BDA (Bluetooth Device Address) for your device. The BT address is 6 bytes, for example 20819A10FFEE. By default, the SDK will set a BDA for your device by combining the 7 hex digit device ID with the last 5 hex digits of the host PC MAC address.


- UART<br/>
    - Set to the UART port you want the application to be downloaded. For example 'COM6' on Windows or '/dev/ttyWICED\_HCI\_UART0' on Linux or '/dev/tty.usbserial-000154' on macOS. By default, the SDK will auto detect the port.


- ENABLE_DEBUG<br/>
    - For HW debugging, select the option '1'. See the document [WICED-Hardware-Debugging](https://github.com/cypresssemiconductorco/btsdk-docs/blob/master/docs/BT-SDK/WICED-Hardware-Debugging.pdf) for more information. This setting configures GPIO for SWD.
      - CYW920819EVB-02/CYW920820EVB-02: SWD signals are shared with D4 and D5, see SW9 in schematics.
      - CYBT-213043-MESH/CYBT-213043-EVAL: SWD signals are routed to P12=SWDCK and P13=SWDIO. Use expansion connectors to connect VDD, GND, SWDCK and SWDIO to your SWD Debugger probe.
      - CYW989820EVB-01: SWDCK (P02) is routed to the J13 DEBUG connector, but not SWDIO. Add a wire from J10 pin 3 (PUART CTS) to J13 pin 2 to connect GPIO P10 to SWDIO.
      - CYW920719B2Q40EVB-01: PUART RX/TX signals are shared with SWDCK and SWDIO. Remove RX and TX jumpers on J10 when using SWD. PUART and SWD cannot be used simultaneously on this board unless these pins are changed from the default configuration.
      - CYW920721B2EVK-02: SWD hardware debugging supported. SWD signals are shared with D4 and D5, see SW9 in schematics.
      - CYW920721B2EVK-03: SWD hardware debugging is not supported.
      - CYW920706WCDEVAL: SWD debugging requires fly-wire connections. The default setup uses P15 (J22 pin 3) for SWDIO and P30 (J19 pin 2) for SWDCK. P30 is shared with BTN1.
      - CYW920735Q60EVB-01: SWD hardware debugging supported. The default setup uses the J13 debug header, P3 (J13 pin 2) for SWDIO and P2 (J13 pin 4) for SWDCK.  They can be optionally routed to D4 and D4 on the Arduino header J4, see SW9 in schematics.
      - CYW920835REF-RCU-01: SWD hardware debugging is not supported.
      - CYW9M2BASE-43012BT: SWD hardware debugging is not supported.

## Downloading an application to a board

If you have issues downloading to the board, follow the steps below:
- Press and hold the 'Recover' button on the board.
- Press and hold the 'Reset' button on the board.
- Release the 'Reset' button.
- After one second, release the 'Recover' button.

Note, this is only applicable to boards that download application images to FLASH storage. Boards that only support RAM download (DIRECT_LOAD) such as CYW9M2BASE-43012BT can be power cycled to boot from ROM.

## Using BSP (platforms)

All BSPs supported by BTSDK can be found in the \wiced_btsdk\dev-kit\bsp\ folder.

#### a. Selecting an alternative BSP

The application makefile has a default BSP. See "TARGET". The makefile also has a list of other BSPs supported by the application. See "SUPPORTED_TARGETS". To select an alternative BSP, set TARGET as one of the supported BSPs.

#### b. Custom BSP

**Complete BSP**

To create and use a complete custom BSP that you want to use in applications, perform the following steps:

1. Select an existing BSP you wish to use as a template from the list of supported BSPs in the \wiced\_btsdk\dev-kit\bsp\ folder.
2. Make a copy in the same folder and rename it. For example \wiced\_btsdk\dev-kit\bsp\TARGET\_mybsp.<br/>
   **Note:** This can be done in the system File Explorer and then refresh the workspace in Eclipse to see the new folder.  Delete the .git sub-folder from the newly copied folder before refreshing in Eclipse.
   If done in the IDE, an error dialog may appear complaining about items in the .git folder being out of sync.  This can be resolved by deleting the .git sub-folder in the newly copied folder.

3. In the new \wiced\_btsdk\dev-kit\bsp\TARGET\_mybsp folder, rename the existing/original (BSP).mk file to mybsp.mk.
4. In the application makefile, set TARGET=mybsp and add it to SUPPORTED\_TARGETS as well as TARGET\_DEVICE\_MAP.  For example: mybsp/20819A1
5. Update design.modus for your custom BSP if needed using the **Device Configurator** link under **Configurators** in the Quick Panel.
6. Update the application makefile as needed for other custom BSP specific attributes and build the application.

**Custom Pin Configuration Only - Multiple Apps**

To create a custom pin configuration to be used by multiple applications using an existing BSP that supports Device Configurator, perform the following steps:

1. Create a folder COMPONENT\_(CUSTOM)\_design\_modus in the existing BSP folder. For example \wiced\_btsdk\dev-kit\bsp\TARGET\_CYW920819EVB-02\COMPONENT\_my\_design\_modus
2. Copy the file design.modus from the reference BSP COMPONENT\_bsp\_design\_modus folder under \wiced\_btsdk\dev-kit\bsp\ and place the file in the newly created COMPONENT\_(CUSTOM)\_design\_modus folder.
3. In the application makefile, add the following two lines<br/>
   DISABLE\_COMPONENTS+=bsp\_design\_modus<br/>
   COMPONENTS+=(CUSTOM)\_design\_modus<br/>
   (for example COMPONENTS+=my\_design\_modus)
4. Update design.modus for your custom pin configuration if needed using the **Device Configurator** link under **Configurators** in the Quick Panel.
5. Building of the application will generate pin configuration source code under a GeneratedSource folder in the new COMPONENT\_(CUSTOM)\_design\_modus folder.

**Custom Pin Configuration Only - Per App**

To create a custom configuration to be used by a single application from an existing BSP that supports Device Configurator, perform the following steps:

1. Create a folder COMPONENT\_(BSP)\_design\_modus in your application. For example COMPONENT\_CYW920721B2EVK-03\_design\_modus
2. Copy the file design.modus from the reference BSP under \wiced\_btsdk\dev-kit\bsp\ and place the file in this folder.
3. In the application makefile, add the following two lines<br/>
   DISABLE\_COMPONENTS+=bsp\_design\_modus<br/>
   COMPONENTS+=(BSP)\_design\_modus<br/>
   (for example COMPONENTS+=CYW920721B2EVK-03\_design\_modus)
4. Update design.modus for your custom pin configuration if needed using the **Device Configurator** link under **Configurators** in the Quick Panel.
5. Building of the application will generate pin configuration source code under GeneratedSource folder in your application.


## Using libraries

All supported libraries (middleware) can be found in the \wiced\_btsdk\dev-kit\libraries folder. To use a library in your application, do the following changes to the makefile in your application:

1. Update the makefile variable "COMPONENTS" to include the library.  For example:<br/>
   COMPONENTS += fw\_upgrade\_lib

2. Update the makefile variable "SEARCH\_LIBS\_AND\_INCLUDES" to point to the location of the library.  For example:<br/>
SEARCH\_LIBS\_AND\_INCLUDES+=$(CY\_SHARED\_PATH)/dev-kit/libraries/btsdk-ota

## Documentation

BTSDK API documentation is available [online](https://cypresssemiconductorco.github.io/btsdk-docs/BT-SDK/index.html)

Note: For offline viewing, git clone the [documentation repo](https://github.com/cypresssemiconductorco/btsdk-docs)

BTSDK Technical Brief and Release Notes are available [online](https://community.cypress.com/community/software-forums/modustoolbox-bt-sdk)
