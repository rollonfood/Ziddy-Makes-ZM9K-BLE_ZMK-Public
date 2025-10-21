## Build Locally
> ⚠️ Tested on MacOS Only

### Preprerequisites
```bash
brew install cmake ninja gperf python3 python-tk ccache qemu dtc libmagic wget openocd
```

Link with more info about building with ZMK and Zephyr, natively on your system
https://zmk.dev/docs/development/local-toolchain/setup/native

You can also you use ZMK's vscode docker devcontainer to build
https://zmk.dev/docs/development/local-toolchain/setup/container

### 1) One Time Setup
```bash
# Start Python Venv
python3 -m venv .venv
source .venv/bin/activate

# Get West Dependencies
pip install west
cd config
west init -l
cd ..
west update
## Install Zephyr's Python Build Tools
pip install -r zephyr-rtos/scripts/requirements.txt
source zephyr-rtos/zephyr-env.sh
# now run build commands or whatever
```


### 2) Every time you start a new terminal:
```bash
# From root of repo
source .venv/bin/activate
source zephyr-rtos/zephyr-env.sh
```


### 3) Build/Compile

✅ On successful builds, the firmware will be built and located in the `build/zephyr/zmk.uf2` file

#### Onboard nRF52840 (no top microcontroller)
```bash
west build -s zmk/app -p -b zm_ble -S studio-rpc-usb-uart -- -DSHIELD="zm9k_ble_c" -DZMK_EXTRA_MODULES=${PWD} -DCONFIG_ZMK_STUDIO=y
```
- ***Info***
  - Custom nRF52840 board
  - Custom `zm9k_ble_c` shield
  - Studio RPC USB UART + ZMK Studio

<br>

---
<br>

#### Nice Nano V2 Clone (microcontroller on top)
```bash
west build -s zmk/app -p -b nice_nano_v2 -S studio-rpc-usb-uart -- -DSHIELD="zm9k_c" -DZMK_EXTRA_MODULES=${PWD} -DCONFIG_ZMK_STUDIO=y
```
- ***Info***
  - nRF52840 Nice Nano V2 Clone
  - Custom `zm9k_ble_c` shield
  - Studio RPC USB UART + ZMK Studio

