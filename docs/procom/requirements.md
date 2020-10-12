[Back to index](./index.md)

# Startup requirements

- Connect the Device via MicroUSB cable to Windows host PC. Green LED1 should light up.
- Generic USB Hub device should install and device manager should show *one* new unknown device
- FTDI USB Serial converter device should install if any FTDI driver has already been installed once

## USB Hub

VID: `0x0424` PID: `0x2514`

No need to do anything.

## Installing device drivers for FT232HL

VID: `0x0403` PID: `0x6014`

Write Device driver using Zadig:

- Start up the Zadig utility

- Select `Options/List All Devices`, then select the FTDI devices you want to communicate with. Its names depends on your hardware, i.e. the name stored in the FTDI EEPROM.

- With FTDI devices with multiple channels, such as FT2232 (2 channels) and FT4232 (4 channels), you **must** install the driver for the composite parent, **not** for the individual interfaces. If you install the driver for each interface, each interface will be presented as a unique FTDI device and you may have difficulties to select a specific FTDI device port once the installation is completed. To make the composite parents to appear in the device list, uncheck the `Options/Ignore Hubs or Composite Parents` menu item.

- Be sure to select the parent device, i.e. the device name should not end with (Interface N), where N is the channel number. For example *Dual RS232-HS* represents the composite parent, while *Dual RS232-HS (Interface 0)* represents a single channel of the FTDI device. Always select the former.

- Select `libusb-win32` (not `WinUSB`) in the driver list.

- Click on `Replace Driver`

## Cypress Chip

VID: `0x04B4` PID: `0x8613`

Install drivers:

- install driver inf from Driver.zip for Windows 10 x64 (or appropriate)
  - device shows as `Cypress FX2LP No EEPROM Device` under USB Devices

- using Cypress USB Control Center, flash EEPROM with `iic` file.
  - new VID/PID will be `0x1d50` and `0x608d`
  - use Zadig to install `WinUSB` driver
  - device will be usable in sigrok as `sigrok FX2 LA (16ch)`
  - PB0..7 correspond to CH0..7 and PD0..7 to CH8..15

## References

[Cypress Driver](https://community.cypress.com/docs/DOC-12366)

[Cypress USB Control Center (Part of SDK)](https://www.cypress.com/documentation/software-and-drivers/ez-usb-fx3-software-development-kit)

[Cypress EEPROM flashing procedure](https://community.cypress.com/docs/DOC-18867)

[Cypress CY7C68013A Datasheet](https://www.cypress.com/file/138911/download)

[FTDI FT232H Datasheet](https://www.ftdichip.com/Support/Documents/DataSheets/ICs/DS_FT232H.pdf)

[Microchip USB2514B Datasheet](http://ww1.microchip.com/downloads/en/DeviceDoc/00001692C.pdf)

[Sigrok Pulseview](https://sigrok.org/wiki/PulseView)

[Sigrok FW API](https://sigrok.org/gitweb/?p=libsigrok.git;a=blob;f=src\hardware\fx2lafw\api.c;h=04efcf3f6abba45d47dab0a2974a8f3c56c97e90;hb=HEAD)

[Zadig 2.5](https://zadig.akeo.ie/)