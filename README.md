# OTA System Design for STM32

### 1. Update modes and update triggers.
- automatic updates : the device periodically checks the server on a daily or weekly basis, or on power on.
- manual updates : the user can manually download an update.

### 2. communication types.

#### A. cellular (preffered communication type)

- hardware : STM32, Cellular module, SIM card
- software : AT parser, HTTP/MQTT/FTP/adaptive protocol selection client over cellular TCP/IP
 
#### B. WiFi

- hardware : STM32, WiFi module(esp32)
- software : HTTP client

#### C. BLE

- hardware : STM32 with inbuilt BLE or with external Bluetooth module
- software : GATT server/client profile

### 3. Functional seperation

#### A. software

- bootloader : handles flash erase/write, CRC check, and application jump. 
- application : periodically triggers OTA check or responds to external update commands. 
- module updater logic : handles network communication, firmware download, and framing

#### B. hardware

- STM32
- flash memory, internal or external
- GPIO for manual update trigger
- Communication module