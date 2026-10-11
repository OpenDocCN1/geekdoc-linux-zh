+   - ISA: Floppy disk controller
+   - ISA: IDE controller
+   - ISA: Motherboard
+   - ISA: PS/2 Mouse
+       - more listed here --
+   - ISA: PnP bios: ECP 1.x compatible parallel port
+   - ISA: System keyboard (US-English)

When you press the F4 key, you display the Device Tasks screen, which lets you view and alter the following device characteristics:

+   - View/Edit Devices
+   - Set Keyboard Configuration
+   - Save Configuration
+   - Delete Saved Configuration
+   - Set Console Device

The default settings are generally best. When you press the F2 key in the Identified Devices screen, the Solaris installer begins to load the device drivers that are appropriate for each specific device that was discovered by the DCA. The process of installing drivers can take up to a few minutes, depending upon the complexity of the system, but once the drivers are loaded, you will see a list of the devices the Solaris installer has prepared that can boot the Solaris 8 operating system. Typically, that list contains a hard drive and a CD-ROM drive in the following format:

```
```
[] DISK: Target 0, (Manufacturer and Model are listed) on ISA bus at (location listed)
```
```

```
```
[] CD : Target 0, Manufacturer and Model are listed) on ISA bus at (location listed)
```
```

To set the boot device, do the following:

+   1. Press the F4 key at the Boot Solaris screen.
+   2. In the Boot Tasks screen, select View/Edit Autoboot Settings and press the F2 key to view any devices from which you can boot Solaris.
+   3. Select the boot device desired and press the F2 key again to return to the View/Edit Autoboot Settings screen.
+   4. Select the Set Autoboot (ON/OFF) command, press the F2 key, and select the ON setting.
+   5. Press the F2 key to return to the View/Edit Autobooot Settings screen.
+   6. Select Accept Settings and press the F2 key.