# ChipIgnite Bringup FW for OpAmp Testing

Simple Blink for Chip Ignite CI2311 to configure GPIO[26:21] as analog for OpAmp testing

## Firmware

You will need python 3.6 or later.  

To program Caravel, connect the evaluation board using a USB micro B connector.

```bash
pip3 install pyftdi

cd firmware/chipignite/blink

make clean flash
```

### Install Toolchain for Compiling Code

#### For Mac

https://github.com/riscv/homebrew-riscv

#### For Linux

https://github.com/riscv/riscv-gnu-toolchain

### Diagnostics

Makefiles in the firmware project directories use 

> util/caravel_hkflash.py 

to program the flash on the board through Caravel's housekeeping SPI interface.

> util/caravel_hkdebug.py 

provides menu-driven debug through the housekeeping SPI interface for Caravel.

### Running the example firmware Blink

The `blink` directory contains example firmware for programming the RISC-V processor with a simple program to flash the
LED connected to the management gpio.

Ensure that you have installed the toolchain for compiling for the RISC-V processor.  You may need to update the 
TOOLCHAIN_PATH variable in the Makefile to point to the location for your tools.

Also make sure you have a current version of python and installed the `pyftdi` library described above.  This is 
required by the utility for programming the onboard flash.

To start, run... 

> make clean hex

to build the firmware.  Program the flash on the development board...

> make flash

Press reset to restart execution.  After a few seconds, you should see the LED for the mgmt GPIO begin to blink slowly.
