
to the U.S. keyboard layout. So instead of her having to learn a new layout, I just configured her login to use the U.S. layout and mine to use the U.K. layout, which has saved us from a number of arguments!

However, you can also use the Keyboard Layout tool to configure special key behaviors. For instance, some people prefer to swap the Caps-Lock and left Ctrl key around. You can set this option and others in the Layout Options tab. If you are not yet a 133t hacker, experiment with what’s on offer; you may get some benefit from these customizations.

Finally, Ubuntu can also configure and enforce typing breaks, all in the name of good health. Simply set the length of working time, the duration of the break, and whether you want to be able to postpone. When this is activated at the end of the first length of working time, Ubuntu locks the computer and will not let you log back in until the break duration has passed. Of course, if you are in the middle of something important, setting the Postpone option may prove useful.

## Mouse

There’s not really much to configuring a mouse. Ubuntu does a great job of detecting most mice, except that it’s not so good at configuring extra buttons over and above the left and right button and scroll wheel. The most useful option here is the Locate Pointer option, which highlights the mouse pointer when you press the Ctrl key. Of course, if you are left-handed, you can also swap the mouse buttons over, but this is a matter of personal preference.

## Detecting and Configuring a Modem

More than 38 million users in the United States and another 85 million users around the world now connect to the Internet with cable or digital subscriber line (DSL) service, but for many users a modem is the standard way to connect with an Internet service provider (ISP) using the Point-to-Point Protocol (PPP). Other common tasks for modems include sending and receiving faxes. If you add or change your modem after the initial installation, you must configure Ubuntu to use the new modem to perform all these tasks.

Ubuntu includes several tools you can use to configure and use an internal or external modem in your notebook or PC. Chapter 18, “Network Connectivity,” contains the details about configuring Ubuntu to connect to the Internet using a modem. This section covers how to configure and use modems using serial ports (using a standard formerly known as RS232, but now called EIA232) or USB.

## Configuring a Serial-Port Modem

Linux uses /dev/ttySX, /dev/ttyUSBX, or /dev/usb/ttyUSBX for serial ports, where X can range from 0 to 15. You can add many additional ports to a system using multiport cards or chained USB devices. A PC’s integral serial ports are generally recognized at boot time.

To see a list of recognized ports for your system, pipe the dmesg command output through the fgrep command, as follows:

```
$ sudo dmesg | grep tty
ttyS00 at 0x03f8 (irq = 4) is a 16550A
ttyS01 at 0x02f8 (irq = 3) is a 16550A
```

In this example, the grep command reports that two serial ports have been recognized in the dmesg output. Note that the device matching ttyS00 is /dev/ttyS0, despite the kernel output. The PC's external modem can be attached (most likely using a male DB9 adapter) to either port. Under Linux, nearly all modem-dependent software clients look for a symbolic link named /dev/modem that points to the desired device. This link is not created by default; as root, however, you can create this device manually using the ln command like this:

```
$ sudo ln -s /dev/ttyS0 /dev/modem
```

In this example, /dev/modem will point to the first serial port.

Ubuntu's network-admin (shown in Figure 4.12) will always detect the presence of a modem on the system. However, it does not activate the interface unless specifically told to do so. You can use the Auto-Detect button to find the correct modem port.

![](img/e464b828c497c99e41f61d4c55f1c0db_107_0.png)

FIGURE 4.12 Ubuntu's network-admin will help you set up an appropriate modem.

## Configuring WinModems for Laptops

Other issues regarding modems focus on Linux notebook users with laptops using controllerless modems. These modems use proprietary software to emulate a hardware
