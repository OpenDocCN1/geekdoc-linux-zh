choose to either allow the system to boot its default configuration, which in this example would be the local hard disk, or to type in the word `linux` and press Enter, which would load the LTSP thin client.

```
DEFAULT localboot
TIMEOUT 50
PROMPT 1
DISPLAY display.msg

LABEL linux
    KERNEL vmlinuz
    APPEND ro initrd=initrd.img quiet splash

LABEL localboot
    LOCALBOOT 0
```

Let’s take a look at the configuration file and break it down so that you can create your own to suit your environment. (If this sample file fits the bill for you, you can skip down to the part about creating the display.msg file.)

The DEFAULT keyword specifies which boot option will be chosen once the timeout expires. The TIMEOUT option specifies how long to wait before booting the default option. This timeout is measured in one-tenth of a second; thus a value of 50 sets it for 5 seconds. The PROMPT option specifies whether the PXE software displays the boot: prompt to enable users to choose an operating system. The DISPLAY option displays a text file on the screen as an introduction. In this case, the file is called display.msg and must be placed in the root LTSP directory alongside the pxelinux.0 file. An example of this file is proposed a little later.

The three lines starting with *LABEL linux* define the *linux* option for booting. This is configured by the KERNEL and APPEND options, which you will notice are extracted from the original default file, as shown here:

```
DEFAULT vmlinuz ro initrd=initrd.img quiet splash
```

All that is needed now is the option for booting from the local hard drive, shown by the two lines starting LABEL localboot. These lines define the localboot option as used with the DEFAULT keyword earlier in the file. The only definition included in this option is the LOCALBOOT option, with a