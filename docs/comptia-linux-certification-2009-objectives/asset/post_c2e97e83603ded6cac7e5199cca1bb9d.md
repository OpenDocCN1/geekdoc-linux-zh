
## Viewing Hardware Details

Some commands that are frequently used for viewing hardware details are listed in the following table.

| Command | Used To |
| :--- | :--- |
| dmesg | View bootup messages. |
| /bin/lsPCI | View information about PCI cards. |
| /bin/lsdev | View information about the installed hardware. |
| /bin/lsmod | View a list of loaded modules. |
| /bin/uname | View system information such as the kernel name, release and version numbers, hardware platform, and operating system. |

## How to Troubleshoot Hardware Issues

### Procedure Reference: Troubleshoot Sound Card Problems

1. Verify that the speaker is connected, switched on, and is functioning.
2. If the speaker is functioning but the problem persists, verify that the sound card is detected while booting.
   - a. Verify that the sound card is listed in the output of the `lsPCI` command.
   - b. If the sound card is not detected, contact your hardware engineer to resolve the sound card issue.
3. If the sound card is detected and the problem still persists, verify that the sound card module is loaded.
   - a. Verify that the sound card module details are listed in the output of the `lsmod` command.
     lsmod module name
   - b. If the sound card module is not loaded, add an entry for the sound card in the /etc/modprobe.conf file. To add an entry in the file, you need to know the slot number and the name of the module used for the sound card.
     alias sound-slot-{slot number} {module name}

![](img/477ccb2f05b6ba1b2d563ea74f18c197_807_0.png)

The /lib/modules/(kernel version)/kernel/sound directory contains modules for the sound card.

   - c. Reboot the system to load the module automatically.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_807_1.png)

You can also load the module using the modprobe or insmod command. If you want to use the modprobe command, run the depmod command to build or update a module database.

### Procedure Reference: Troubleshoot Modem Issues

To troubleshoot the modem issues:

1. Verify that the modem is connected properly to the system and powered on.
2. Check your telephone line and verify that it is connected properly to the modem.
3. Verify that the modem speed is set properly.
   - a. Verify that the modem speed specified in the /etc/mgetty+sendfax/mgetty.config file is equal or less than your modem speed.
   - b. If the modem speed is not set, modify the speed parameter in the file.

```
speed speed in bps
```

4. Verify that the serial port settings are correct.
   - a. Verify that the settings listed in the output of the setserial -a /dev/ttyS0 command matches with your modem specifications.
   - b. If the serial port settings are not proper, change them.

```
setserial /dev/ttyS{port number} {spd_normal | spd_hi | spd_vhi}
setserial /dev/ttyS{port number} baud_base {baud rate}
```

5. If you are still unable to dial using the modem, then the issue is hardware related. Contact your hardware engineer to resolve the issue.

### Procedure Reference: Troubleshoot LCD Panel Issues

To troubleshoot the LCD panel issues:

1. Verify that the LCD panel is connected to the system properly and is powered on.
2. Verify that the VGA card module is configured correctly.
   - a. Verify that all parameters in the Screen section in the /etc/X11/xorg.conf file are entered correctly.
   - b. If necessary, modify the parameters according to your LCD panel specifications.
3. Verify that the monitor parameters such as DefaultDepth, Viewport, and Depth are configured correctly.
   - a. In the /etc/X11/xorg.conf file, verify that the DefaultDepth, Viewport, and Depth parameters are set properly.
   - b. If necessary, modify the parameters according to your LCD panel specifications.
4. If the LCD monitor is still not working properly, then the issue is hardware related. Contact your hardware engineer to resolve the issue.

### Procedure Reference: Troubleshoot Dumb Terminal Issues

To troubleshoot the dumb terminal issues:

1. Verify that the dumb terminal device is connected properly to the server.
2. Verify that the serial port is configured correctly.
   - a. Verify that the settings listed in the output of the `setserial -a /dev/ttyS0` command matches your device specifications.
   - b. If necessary, change the serial port settings.

```
setserial /dev/ttyS{port number} {spd_normal | spd_hi | spd_vhi}
setserial /dev/ttyS{port number} baud_base {baud rate}
```

3. If the dumb terminal is still not working properly, then the issue is hardware related. Contact your hardware engineer to resolve the issue.

### Procedure Reference: Troubleshoot Issues Related to UPS Devices

To troubleshoot issues related to UPS devices:

1. Verify that the UPS device is connected properly to the server.
2. Verify that the serial port is configured correctly.
   - a. Verify that the settings listed in the output of the `setserial -a /dev/ttyS0` command matches your device specifications.
   - b. If necessary, change the serial port settings.

```
setserial /dev/ttyS{port number} {spd_normal | spd_hi | spd_vhi}
setserial /dev/ttyS{port number} baud_base {baud rate}
```

3. If the UPS device is still not working properly, then the issue is hardware related. Contact your hardware engineer to resolve the issue.

### Procedure Reference: Troubleshoot Mouse Issues

To troubleshoot mouse issues:

1. Verify that the mouse is connected properly to the system.
2. Reboot the system.
3. If the mouse is still not working, then the issue is hardware related. Contact your hardware engineer to resolve the issue.

### Procedure Reference: Troubleshoot Floppy Disk Problems

To troubleshoot floppy disk issues:

1. Verify that the power connector to the floppy drive is proper.
   - If the connection is not powered on, then there is a problem with the power connector.
   - a. Verify that the read-write indicator is glowing.
   - b. If it is not glowing, the power connector needs to be checked and replaced.
2. If the power connector is working and the floppy issue persists, then there is a problem with the floppy drive or the floppy.
   - a. With your hardware engineer’s help, verify that the floppy drive is functioning properly.
   - b. If the floppy drive is functional, verify that your floppy is functioning properly.

### Procedure Reference: Troubleshooting X

To troubleshoot X:

1. Switch to runlevel 3.
2. Check that the required criteria for X are met.
   - Ensure that the quota value for the user has not been reached.
   - Enter `service xfs status` to check whether the xfs font server is running.
   - Enter `X -probeonly` to gather more information.
   - Make sure that the host name of the system is configured properly.
   - Enter `system-config-display` to check whether the display settings are configured properly.

## DISCOVERY ACTIVITY 16-4

## Troubleshooting Hardware Issues

**Scenario:**
Your company organized a trade show, where you set up several dumb terminals with LCD monitors to demonstrate your company's products. You are responsible for troubleshooting any hardware-related issues.

1. In which file will you change the LCD monitor parameters such as DefaultDepth, Viewport, and Depth?
   a) /etc/X11Config
   b) /etc/XF86
   c) /X11/XF86Config
   ✓ d) /etc/X11/xorg.conf

2. One of the LCD monitors is not displaying any output. What could be the problem? Select all that apply.
   ✓ a) The LCD panel is not connected properly to the system.
   ✓ b) The VGA card module is not configured properly.
   c) Serial port settings are not configured properly.
   ✓ d) Monitor parameters, such as DefaultDepth, Viewport, and Depth, are not configured properly.

3. True or False? In the /etc/X11/xorg.conf file, the section Screen contains parameters of the VGA card module for an LCD monitor.
   √ True
   __ False

4. In one of the terminals, users are not able to listen to the audio associated with the animation. What will be your first step to troubleshoot the issue?
   a) Verify that the sound card is detected while booting.
   b) Verify that the sound card module is loaded.
   c) Contact the hardware engineer to solve the issue.
   ✓ d) Verify that the speaker is connected, switched on, and working properly.
