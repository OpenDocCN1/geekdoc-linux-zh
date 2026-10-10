Udev also handles coldplug. Because udev is part of user space and is started only after the kernel boots, a special mechanism is needed to emulate hotplug events over coldplugged devices. At boot time, the kernel creates a file named `uevent` under `sysfs` for all devices and emits coldplug events to those files. When udev starts, it reads all the `uevent` files from `/sys` and generates hotplug events for each coldplugged device.

# Microcode Download

You have to feed microcode to some devices before they can get ready for action. The microcode gets executed by an on-card microcontroller. Device drivers used to store microcode inside static arrays in header files. But this has become untenable because microcode is usually distributed as proprietary binary images by device vendors, and that doesn't mix homogeneously with the GPL-ed kernel. Another reason against mixing firmware with kernel sources is that they run on different release time lines. The solution apparently is to separately maintain microcode in user space and pass it down to the kernel when required. Sysfs and udev provide an infrastructure to achieve this.

Let's take the example of the Intel PRO/Wireless 2100 WiFi mini PCI card found on several laptops. The card is built around a microcontroller that needs to execute externally supplied microcode for normal operation. Let's walk through the steps that the Linux driver follows to download microcode to the card. Assume that you have obtained the required microcode image (`ipw2100-1.3.fw`) from `http://ipw2100.sourceforge.net/firmware.php` and saved it under `/lib/firmware/` on your system and that you have inserted the driver module `ipw2100.ko`.

+   1.  During initialization, the driver invokes the following:
+   
+   ```
+   request_firmware(..., "ipw2100-1.3.fw", ...);
+   ```

+   2.  This dispatches a hotplug uevent to user space, along with the identity of the requested microcode image.

+   3.  Udevd receives the uevent and responds by invoking `/sbin/firmware_helper`. For this, it uses a rule similar to the following from a file under `/etc/udev/rules.d/`:
+   
+   ```
+   ACTION=="add", SUBSYSTEM=="firmware", RUN="/sbin/firmware_helper"
+   ```

+   4.  `/sbin/firmware_helper` looks inside `/lib/firmware/` and locates the requested microcode image `ipw2100-1.3.fw`. It dumps the image to `/sys/class/0000:02:02.0/data`. (`0000:02:02` is the PCI bus:device:function identifier of the WiFi card in this case.)

+   5.  The driver receives the microcode and downloads it onto the device. When done, it calls `release_firmware()` to free the corresponding data structures.

+   6.  The driver goes through the rest of the initializations and the WiFi adapter beacons.

# Module Autoload

Automatically loading kernel modules on demand is a convenient feature that Linux supports. To understand how the kernel emits a "module fault" and how udev handles it, let's insert a Xircom CardBus Ethernet adapter into a laptop's PC Card slot.