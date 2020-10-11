[Back to index](./index.md)

## Startup requirements

- Connect the Device via MicroUSB cable to Windows host PC. Green LED1 should glow.
- Generic USB Hub device should install and device manager should show *one* new unknown devices 
- FTDI USB Serial converter device should install

#### Problems:

- EEPROM currently not detected using FT_PROG / FTDI not working
  - USB Hub not able to deliver enough current to FTDI
- ~~FT232H not visible on startup~~
  - Crystal line was shorted to VDD

### Writing configuration to the EEPROM

Write FTDI FT232HL EEPROM data using [FT_Prog_v3.10.132.511](https://www.ftdichip.com/Support/Utilities.htm#FT_PROG)


### Installing device drivers fot FT232HL

Vendor ID: 0403
Device ID: 6014

Write Device driver using [Zadig 2.5](https://zadig.akeo.ie/)

1. Start up the Zadig utility

2. Select `Options/List All Devices`, then select the FTDI devices you want to communicate with. Its names depends on your hardware, i.e. the name stored in the FTDI EEPROM.

  - With FTDI devices with multiple channels, such as FT2232 (2 channels) and FT4232 (4 channels), you **must** install the driver for the composite parent, **not** for the individual interfaces. If you install the driver for each interface, each interface will be presented as a unique FTDI device and you may have difficulties to select a specific FTDI device port once the installation is completed. To make the composite parents to appear in the device list, uncheck the `Options/Ignore Hubs or Composite Parents` menu item.

  - Be sure to select the parent device, i.e. the device name should not end with (Interface N), where N is the channel number.

    - for example *Dual RS232-HS* represents the composite parent, while *Dual RS232-HS (Interface 0)* represents a single channel of the FTDI device. Always select the former.

3. Select `libusb-win32` (not `WinUSB`) in the driver list.

4. Click on `Replace Driver`

### Cypress Chip

Vendor ID: 04B4
Device ID: 8613