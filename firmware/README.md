# Firmware

Runs on Klipper. Currently requires manual flashing via SD card or over UDF (USB).

## Configurations

### Octopus Pro V1.1

Copy the resulting `out/klipper.bin` to a FAT32 formatted sd-card
with the name `FIRMWARE.BIN` and insert the card in the mainboard.

Press the RESET switch next to the slot and wait for 30 seconds before
removing the card and pressing again.

```bash
make clean
make KCONFIG_CONFIG=octopus.kconfig menuconfig
make KCONFIG_CONFIG=octopus.kconfig
cp out/klipper.bin /mnt/sd-card/firmware.bin
```

### Voron Klipper Expander

Place the BOOT jumper into place and press the RESET button to enter DFU
mode. The device should show up in `lsusb`.

```bash
make clean
make KCONFIG_CONFIG=expander.kconfig menuconfig
make KCONFIG_CONFIG=expander.kconfig
make KCONFIG_CONFIG=expander.kconfig flash FLASH_DEVICE=0483:df11
```

### Host

Reset the host after flashing.

```bash
make clean
make KCONFIG_CONFIG=host.kconfig menuconfig
make KCONFIG_CONFIG=host.kconfig
make KCONFIG_CONFIG=host.kconfig flash
```

### Cartographer

The software from https://github.com/Cartographer3D/cartographer-klipper includes
a CLI tool to update the firmware:

* DFU: https://docs.cartographer3d.com/cartographer-probe/firmware/firmware-updating/via-dfu
* Katapult: https://docs.cartographer3d.com/cartographer-probe/firmware/firmware-updating/via-katapult/usb-flash
