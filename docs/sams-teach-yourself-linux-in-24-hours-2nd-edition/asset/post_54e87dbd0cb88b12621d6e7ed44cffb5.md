
- A command-line shell dialog box for running commands, which displays output in the main communication window
- Buttons to set up modem speed, parity, and stop bits

If you created a symbolic link to /dev/modem, the seyon program automatically recognizes and works with your modem. All you have to do to call out and connect with another computer is to type your AT command string with the phone number to dial out and connect.

If you need to tell the seyon client the specific device for your modem, click on the Set button in the seyon Command Center window (which appears automatically when you start the client) to bring up the Settings window. Click on the Port button in the Settings window, and type in the name of the device, /dev/cua1 for example, in the Values? window. Figure 9.7 shows seyon and its settings windows.

## FIGURE 9.7

The X11 client, seyon, has point-and-click convenience for modem setup.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_228_0.png)

Main seyon window

Main seyon controls

Help window

Baud rate settings

Communication settings

Click on the OK button, and click on the Close button of the Settings window. If you want to start the seyon program with a default modem speed, number of bits, or parity, edit the file $HOME/.seyon/. This directory is installed automatically when you install the seyon program. You can make changes to the following lines in the startup file:

```
# set baud
set baud 19200

# can be 5, 6, 7, or 8
# set bits 8
set bits 8

# can be 0 (= no parity), 1 (= odd parity), or 2 (= even parity)
# set parity 0
set parity 0

# can be 1 or 2
# set stopBits 1
set stopBits 1
...
```

If you need help when using the seyon program, you can click on the Help button in the seyon Command Center window. A window pops up with the seyon manual page, and you can scroll through the text for help (the help screen is shown in Figure 9.7).

## Setting Up Your Linux System for Dialing In

You can also set up your OpenLinux system so that your computer's modem answers the phone and enables you to log in. You can then run a bulletin board system (BBS), word processors, and spreadsheet programs. You can even dial out on another line if you have at least two modems connected to your computer and two phone lines in your home.

Most of the details and custom configurations are in the Serial-HOWTO under the /usr/doc/HOWTO and /usr/doc/getty_ps directories, but the three basic steps outlined here should work for nearly any modem.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_229_0.png)

> Setting up your OpenLinux system to accept incoming calls involves editing the /etc/inittab file and can potentially hang your system if you make an error. Always have a backup boot disk handy, and make a copy of the /etc/inittab file before you make changes.

First, log in as the root operator, and run minicom. Use the AT command &V to display your modem's profile, or default setup, for example:

```
AT&V
ACTIVE PROFILE:
B1 E1 L1 M1 N1 Q0 T V1 W0 X4 Y0 &C1 &D2 &G0 &J0 &K3 &O5 &R1 &S0 &T5 &X0 &Y0 -Z0
```

```
S00:000 S01:000 S02:043 S03:013 S04:010 S05:008 S06:004 S07:045 S08:002 S09:006
S10:014 S11:095 S12:050 S18:000 S25:005 S26:001 S36:007 S37:000 S38:020 S44:020
S46:138 S48:007 S51:012 S52:012 S53:010 S54:010 S95:000
```

You might see other values for your modem's internal profile and registers, but you need to make sure that your modem is at least set to the following:

```
E1 Q0 V1 S0=1 &C1 &S0
```

You can set your modem to these values by using the AT command, for example:

```
ATE1Q0V1S0=1&C1&S0&W
OK
```

Note that at the end of the AT command string, using the &W AT command saves the modem configuration as a default. You can also see the OK prompt echoed back to you from your modem after entering the string, and you can again issue the AT&V command to verify the settings.

The second step is to create a directory named default under the /etc directory, like this:

```
# mkdir /etc/default
```

Then, use the cp command to copy the file ugetty.autoanswer from the /usr/doc/getty_ps directory, renaming the file to match your modem's serial port device, like so:

```
# cp /usr/doc/getty_ps-2.0.7h/Examples/ugetty.autoanswer /etc/default/ugetty ttyS0
```

This command line shows that the desired serial port is /dev/ttyS0, which corresponds to the DOS COM1 port. Now edit the copied file with your favorite text editor, and look for the following line:

```
ALTLOCK=cua2
```

Change the default values of cua2 to match the extension and serial port of your modem, like this:

```
ALTLOCK=ttyS0
```

Save the file and exit your editor.

The final step involves a one-line edit of /etc/inittab, the system initialization table. If you look in this file, you see these lines:

```
# less /etc/inittab
...
# Run gettys in standard runlevels
```

```
1:12345:respawn:/sbin/getty tty1 VC linux
2:2345:respawn:/sbin/getty tty2 VC linux
3:2345:respawn:/sbin/getty tty3 VC linux
4:2345:respawn:/sbin/getty tty4 VC linux
5:2345:respawn:/sbin/getty tty5 VC linux
6:2345:respawn:/sbin/getty tty6 VC linux
...
```

Each of the lines represents a different Linux runlevel documented at the beginning of the /etc/inittab file. This discussion doesn't cover runlevels or the details of how OpenLinux boots, but all you have to do to enable dial-in logins for your Linux system is to change the following line:

```
3:2345:respawn:/sbin/getty tty3 VC linux
```

Change it as follows:

```
3:2345:respawn:/sbin/ugetty ttyS0 38400 vt100
```

Save the file, and use the shutdown command to restart your system. This inittab entry tells OpenLinux to start the getty command after you boot and have getty monitor your /dev/ttyS0 serial port for incoming calls. The value 38400 is not a modem baud rate but corresponds to an autobaud entry (which works at 38400 or lower speeds) in the /etc/gettydefs file. If you call in to your OpenLinux system, the modem synchronizes with your calling modem's speed and then presents a login prompt.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_231_0.png)

When you log in to OpenLinux, the contents of the /etc/issue file are printed on your display right before the login prompt. This file is created by the startup script rc.local in the /etc/rc.d directory every time you start OpenLinux as part of the booting process. As the root operator, you can customize the rc.local script to change the contents of the /etc/issue file if you want a different login banner.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_231_1.png)

If you set up your system to accept incoming calls and want to use minicom, run minicom as the root operator. Then configure the serial device name under serial port setup in the configuration menu to match the name of your modem's actual device, such as /dev/ttyS1, and make sure the name is not a symbolic link, such as /dev/modem.

## Sending and Receiving Faxes

If your modem supports fax protocols, chances are that you can send and receive faxes using OpenLinux. Sending and receiving faxes under OpenLinux involves graphics translation of both received files and files you want to send. Your OpenLinux distribution on the CD-ROM contains the efax family of fax software and documentation. Have your modem's documentation on hand and read the efax manual pages and documentation under the /usr/doc/efax directory carefully before you start.

## Faxing with the efax System

The efax system, by Ed Casas, is a simple and easy-to-use fax system that, according to its documentation, is best suited to a single-user, standalone Linux system. This software consists of a series of programs and scripts and supports Class 1 and 2 fax modems.

The system is made up of the following programs:

- `/usr/bin/efax`—The faxing program
- `/usr/bin/efix`—A graphics conversion program used to prepare text files for faxing or to convert files to different graphics formats
- `/usr/bin/fax`—A shell script used to create, send, receive, display, or print fax files

If you want to preview or fax PostScript graphics files, you also need to have the gs PostScript interpreter and companion viewer, gv, installed on your system. For viewing received faxes, you can use the X11 client xv (discussed in Hour 16, “Graphics Tools”).

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_232_0.png)

> You need to edit the /usr/bin/fax script to configure faxing. But before you make changes to the script, do yourself a favor and make a copy first. If you make errors or delete the file, you need a copy to reinstall the efax software.

Before you start sending or receiving faxes, take a look at the /usr/bin/fax shell script. This program is the front-end to fax service with efax, but you need to check several sections in the file to make sure the script is configured properly. For example, the first section lists the names of the efax programs:

```
FAX=/usr/bin/fax
EFAX=/usr/bin/efax
EFIX=/usr/bin/efix
```

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_232_1.png)
