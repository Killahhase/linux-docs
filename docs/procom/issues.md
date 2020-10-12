[Back to index](./index.md)

# Issues

- ~~EEPROM currently not detected using FT_PROG / FTDI not working~~
  - ~~USB Hub not able to deliver enough current to FTDI~~
  - ~~removed R24, R25 (battery charger protocol strap options)~~ **No Effect**
  - **Fixed: changed USB hub config from bus-powered to self-powered by pulling R33 to GND instead of 3V3**
- ~~FT232H not visible on startup~~
  - ~~Crystal line shorted to VDD~~ 
  - **Fixed by removing short**
- ~~VBUS_DET on USB Hub **must not** be connected to 5V directly, connect to 3V3 behind regulator instead!~~ 
  - **Fixed by connecting VBUS_DET to 3V3**