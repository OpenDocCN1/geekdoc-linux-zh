device is used to read the CPU temperature and fan speed on our system. These lines for /etc/modprobe.conf were suggested for our use by the program’s documentation. We added them with a text editor.

```
alias char-major-89 i2c-dev
options eeprom ignore=2,0x50,2,0x51,2,0x52
```

A partial listing of lsmod is shown here, piped through the less command, allowing us to view it a page at a time:

```
# lsmod | less
Module			Size Used by
parport_pc		19392	1
Module			Size Used by
parport_pc		19392	1
lp			8236	0
parport		29640	2 parport_pc,lp
autofs4		10624	0
sunrpc		101064	1
```

The list is actually much longer, but here we see that the input module is being used by the joydev (joystick device) module, but the joystick module is not being used. This computer has a joystick port that was autodetected, but no joystick is connected. A scanner module is also loaded, but because the USB scanner is unplugged, the module is not being used. You would use the lsmod command to determine whether a module was loaded and what other modules were using it. If you examine the full list, you would see modules for all the devices attached to your computer.

To remove a module, joydev in this example, use

```
# rmmod joydev
```

or

```
# modprobe -r joydev
```

A look at the output of lsmod would now show that it is no longer loaded. If we removed input as well, we could then use modprobe to load both input and joydev (one depends on the other, remember) with a simple

```
# modprobe joydev
```

If Fedora Core Linux were to balk at loading a module (because it had been compiled using a different kernel version from what we are currently running; for example, the NVIDIA graphics card module), we could force it to load like this:

```
# insmod -f nvidia
```

We would ignore the complaints (error messages) in this case if the kernel generated any.