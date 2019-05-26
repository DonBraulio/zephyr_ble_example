# Bluetooth: Peripheral HR

## Overview
Example based on `samples/bluetooth/peripheral_hr`, instructions provided for the nRF52840 Development Kit (PCA10056).

## Requirements

- Install nrfjprog (see [Nordic docs](https://infocenter.nordicsemi.com/index.jsp?topic=%2Fug_nrf5x_cltools%2FUG%2Fcltools%2Fnrf5x_nrfjprogexe.html) )
- Install ARM GCC compiler (download from [here](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads))
- Install other system dependencies like indicated [here](https://docs.zephyrproject.org/latest/getting_started/index.html#set-up-a-development-system)
- `pip install west`  (Zephyr's build configuration tool)
- JLink Debugger tool (or `pyocd` if using mbed DAPLink interface firmware)
- JLink or mbed (DAPLink) interface firmware flashed (see [nRF52840-DK downloads](https://www.nordicsemi.com/Software-and-Tools/Development-Kits/nRF52840-DK/Download#infotabs))


Sample configuration for Zephyr's `west` tool:
```bash
export PATH=/usr/local/nRF-Command-Line-Tools_9_8_1_OSX/nrfjprog:$PATH
export ZEPHYR_TOOLCHAIN_VARIANT=gnuarmemb
export GNUARMEMB_TOOLCHAIN_PATH="/usr/local/gcc-arm-none-eabi-8-2018-q4-major"
```

## Building & Debugging

### Using Segger JLink
If you have nrfjprog, JLink debugger and the JLink firmware flashed, you should be able to flash or start a debug session only with this:

```bash
west build -b nrf52840_pca10056
west flash
west debug
```
**Note:** west and zephyr itself are under active development.
If the `west build` command fails in the instructions, try upgrading the *system requirements* indicated above (mainly `cmake`), or compile directly using CMake and Ninja (instead of the west wrapper) as described in the [step 3 of the guide](https://docs.zephyrproject.org/latest/getting_started/index.html#build-the-application).
### Using ARM DAPLink
If ARM mbed DAPLink firmware is flashed in the DK interface, you need to tell `west` to use `pyocd` debugger:
```bash
west build -b nrf52840_pca10056
west flash --runner pyocd --target nrf52840
```

### Serial Loggers
For some reason, `screen` is not showing the console output correctly in my case (OSX), but `minicom` works fine showing all log traces:
```bash
minicom -D /dev/tty.usbmodemXXX -b 115200
```

## Zephyr docs for this board
The Zephyr documentation is great, specific examples for this board can be found [here](https://docs.zephyrproject.org/latest/boards/arm/nrf52840_pca10056/doc/index.html).
