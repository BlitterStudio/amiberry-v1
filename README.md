# AmiBerry
A script to configure a stock [Minibian](https://minibianpi.wordpress.com/) system as a dedicated Amiga emulation machine.

Requirements
------------
- A Raspberry Pi 3 (recommended) or 2.
- A stock [Minibian](https://minibianpi.wordpress.com/) installation.

Usage
-----

~~~ bash
wget --content-disposition https://git.io/v6Oxc
sh ./amigapi
~~~

What next?
----------
The tool will present you with a menu containing all available options.
You should start with expanding the filesystem, Upgrading the system and finally install AmigaPi.
Once you install AmigaPi, the system will be configured to boot straight into UAE.

You can configure your setup and once you're happy, untick the option "Show GUI on startup" in UAE's Miscellaneous page, to boot straight into Workbench from that moment on.
You can always quit UAE to go back to your normal (Linux) login screen.

You can re-run the tool to perform any of the tasks it handles, including upgrading your system, upgrading UAE, enabling/disabling system options as well as the UAE service, etc.

Known issues
------------
- You can freely upgrade the system, but if you upgrade the firmware as well (rpi-update) then uae4arm will break. This problem has been reported to the author of uae4arm (here: https://github.com/Chips-fr/uae4arm-rpi/issues/22), until it's fixed with a new version, please don't upgrade the firmware.

Problems?
---------
- If you're having problems with UAE, please refer to the uae4arm-rpi project page by Chips-fr (https://github.com/Chips-fr/uae4arm-rpi).
- If you find a bug in the amigapi tool, please let me know by opening an Issue on the Github page.

Troubleshooting WiFi
--------------------
If your `wlan0` is not working after rebooting, you're probably missing kernel
firmware for your wireless network adapter.

Just check `dmesg` for entries looking like:

> r8188eu 1-1.5:1.0: **Firmware** _rtlwifi/rtl8188eufw.bin_ **not available**


and use `apt-file` to find the corresponding package containing this firmware:

~~~~ bash
apt-file update
apt-file find rtl8188eufw.bin
~~~~


which will result in:

~~~~ shell
firmware-realtek: /lib/firmware/rtlwifi/rtl8188eufw.bin
~~~~


and then install the required package:

~~~~ bash
apt-get -y install firmware-realtek
~~~~


Now unplug and reinsert the wireless adapter or reboot.
