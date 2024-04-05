# Custom WLED Build for M5Stack Atom Lite with Animated Staircase Usermod (WLED 14.3)

This repository contains a custom WLED firmware build for the M5Stack Atom Lite, featuring specific hardware-related adjustments to optimize performance and compatibility. The primary modifications include a change in the LED pin and the button pin configurations to avoid hardware conflicts and enable the use of the USERMOD_ANIMATED_STAIRCASE feature.

## Modifications

The key changes in this build are as follows:

- **LEDPIN**: Set to `27` to avoid conflict with the `FLASH_CS` pin (`16`).
- **BTNPIN**: Set to `39` for optimal button functionality.
- **Feature**: `USERMOD_ANIMATED_STAIRCASE` has been enabled to enhance the visual effects available on the device.

These adjustments were necessary to ensure that the LED functionality did not interfere with the flash memory operations on the M5Stack Atom Lite.

## Flashing Instructions

To flash this custom firmware onto your M5Stack Atom Lite, follow the steps below. Ensure that you have [esptool.py](https://github.com/espressif/esptool) installed on your computer before proceeding.

1. **Erase the Flash Memory**

   Begin by erasing the entire flash memory of the device to ensure a clean state for the firmware installation.

    ```bash
    esptool.py erase_flash
    ```

2. **Flash the Custom Firmware**

   Proceed to flash the firmware components in the following order, using the specified offsets. Replace `path/to/` with the actual path to each binary file in this repository.

    - **Bootloader**:

        ```bash
        esptool.py --baud 115200 write_flash -fm dout 0x1000 ./bootloader_dout_40m_v2022.bin
        ```

    - **Partition Table**:

        ```bash
        esptool.py --baud 115200 write_flash -fm dout 0x8000 ./partitions_v2022.bin
        ```

    - **boot_app0**:

        ```bash
        esptool.py --baud 115200 write_flash -fm dout 0xe000 ./boot_app0_v2022.bin
        ```

    - **WLED Firmware Image**:

        ```bash
        esptool.py --baud 115200 write_flash -fm dout 0x10000 ./wled-m5atom-lite-staircase.bin
        ```

After flashing all components, restart your M5Stack Atom Lite to apply the changes. The device should now operate with the new firmware, incorporating the custom settings and features detailed above.

## Useful Resources
https://docs.m5stack.com/en/core/atom_lite
https://install.wled.me/
https://serial.huhn.me/
https://wled-install.github.io/
https://wled-compile.github.io/
https://github.com/Aircoookie/WLED/blob/main/usermods/Animated_Staircase/README.md


## Support

If you encounter any issues or have questions regarding this custom build, feel free to open an issue in this repository or reach out for support through the [WLED Discord community](https://discord.gg/wled).

---

Feel free to adjust the content as needed to better fit your project or to add any additional sections that might be helpful for users or contributors.
