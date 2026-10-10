particular, that pretty much every node has a *compatible* property. This is what links a node to the device driver that manages it.

The device tree source code is compiled into a more compact form called a **device tree blob** (`.dtb`), also known as a **flattened device tree** (fdt). As mentioned above, the device tree compiler is actually part of the kernel source tree. The resulting `am335x-boneblack.dtb` is stored in the same flash partition as MLO and `u-boot.img`. The default u-boot environment has a variable, `loadfdt`, that loads the device tree blob into RAM. Then the `bootz` command that transfers control to the kernel has three address arguments: the address of the kernel, the address of the initial RAM disk, and the address of the device tree blob. As the kernel loads device drivers, the drivers interrogate the device tree to determine the specific properties of their respective devices.

The device tree is visible from u-boot using the `fdt` commands. Type `help fdt` to see the commands. Among other things, you can list the fdt, create new nodes and properties, and change property values. Then once the kernel is booted, the device tree is visible at `/proc/device-tree`. This tree is read-only.

# Putting the Application in eMMC Flash

We are almost done. We have configured the kernel and the boot loader to our specific needs. We have set up systemd and/or the init process so that it boots directly into the thermostat application. At the end of the last chapter, we ended up with a file system that booted directly into our networked thermostat application. The final step then is to load that file system into eMMC flash on the target board, so that when the board powers up, the thermostat starts.

The process is actually quite straightforward. You do still have the microSD card with the eMMC flasher image on it, the one we used back in Chapter 6, The hardware, right? Here are the steps then:

+   - Insert the microSD card into your workstation
+   - Mount both partitions, BEAGLEBONE and eMMC-Flasher
+   - Copy any changes from your networked file system to the microSD eMMC-Flasher partition
+   - Restore the original `uEnv.txt` to the BEAGLEBONE partition so the device boots from eMMC
+   - If necessary, copy your new `u-boot.img` and kernel `zImage` files to the BEAGLEBONE partition
+   - Insert the microSD card into your unpowered BBB and power up
+   - The eMMC is flashed with your “production” file system
+   - Power down, remove the microSD card, and power up. Your “product” is now running.