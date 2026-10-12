
System actions (such as rebooting or shutting down), provide shortcuts to save typing, and can aid in reading files or viewing program output.

For example, you can scroll the contents of your screen from the console by pressing Shift+PageUp or Shift+PageDown, and can copy and paste text using your mouse buttons. This section shows you how to access default or custom menus at the text console, which can be helpful to get system information or to launch new programs.

If you use a mouse with Linux (and you most likely do), you can use your pointing device for copy and paste operations. This support is provided by gpm, the general purpose mouse server. The gpm server must be enabled or started while booting Linux (see Chapter 14 for more details in the section “Controlling Services at Boot Using Administrative Tools”). To copy a section of text, click and drag text with the left mouse button (button 1) held down. To paste text, click an insertion point, and then press the middle mouse button (button 2).

Button assignment, like all mouse controls during text console use, is managed by command-line options given to gpm when it is started. For example, if you look at the gpm startup script named gpm under the /etc/rc.d/init.d/ directory, you’ll see that it uses the file named mouse under the /etc/sysconfig directory to hold options:

```
# Additional options for gpm (e.g. acceleration), device
OPTIONS=""
DEVICE="/dev/mouse"
```

You can add options, detailed in the gpm manual page to change how your mouse works, enable or disable features, or assign special commands to a specific mouse button click. For example, to change your button order from 123 (left, middle, and right) to 321, edit the /etc/sysconfig/mouse file as root and change the OPTIONS entry like so:

OPTIONS="-B 321"

After saving your changes, restart gpm like so:

# /etc/rc.d/init.d/gpm restart

Your mouse buttons will now be reversed!

To aid users with a two-button mouse, Linux supports three-button emulation; emulation lets users simultaneously press the right and left mouse buttons to simulate a press of the middle button. You can enable this feature during installation or by using the mouseconfig command. See the section “Configuring Pointing Devices in Linux” in Chapter 4, “Post-Installation Configuration,” to see how to use mouseconfig.

The gpm server also provides the ability to reboot or shut down the system with the mouse. Depending on the combination of mouse buttons you press, you have several reboot or shutdown options. Begin by holding down either the left or right mouse button and triple-clicking the opposite button; depending on which mouse button you press next, one of these actions occurs:

- Pressing the left button causes an immediate reboot using the init command.
- Pressing the middle button reboots the system using the shutdown command.
- Pressing the right button causes the system to shut down immediately with the shutdown command.

You can also create custom menus that will pop up at a text-based Linux console by editing the file /etc/gpm-root.conf (as root) and starting the gpm-root command. When you run gpm-root without making changes to its configuration file, by default a system status dialog (with the date, time, CPU load, free memory, and swap file usage) will appear if you hold down the Ctrl key and press the middle mouse button.

You can change your keyboard layouts by using the loadkeys command. To use a different font for the console, try the setfont command. Fedora Core Linux comes with nearly 150 different console fonts, which are found under the /lib/kbd/consolefonts directory. See the section “Configuring Keyboards with Linux” in Chapter 4 to see how to use these commands.

> **NOTE**
>
> A text-based, dial-up login, also known as a shell account, looks much the same as a text-based login at a PC running Linux. Details about setting up Linux to answer the phone and provide a login prompt via a modem are in Chapter 18. Using dial-up access has some limitations, such as the inability to use virtual consoles. From a shell account, however, you can start programs in the background (using the ampersand, &), run programs after logging out with the nohup command, or use the screen command to simulate virtual terminals (an approach that works much like using virtual consoles). For more information on different shells included with Linux, see Chapter 14.

## Logging Out

Use the exit or logout commands to exit your session. Type the command and press Enter. You’ll then be returned to the login prompt. If you use virtual consoles, remember to exit each console before leaving your PC. (Otherwise, someone could easily sit down and use your account.)

## Logging In and Out from a Remote Computer

Although you can happily log in on your computer, an act known as a local log in, you can also log in to your computer via a network connection from a remote computer. Linux-based operating systems provide a number of remote access commands you can use to log in to other computers on your local area network (LAN), wide area network (WAN), or the Internet. Note that not only must you have an account on the remote computer, but also the remote computer must be configured to support remote logins—otherwise, you won’t be able to log in.

> **NOTE**
>
> See Chapter 17 to see how to set up network interfaces with Linux to support remote network logins and Chapter 14 to see how to start remote access services (such as sshd).

The best and most secure way (barring future exploits) to log in to a remote Linux computer is to use the *ssh* or Secure Shell client. Your login and session are encrypted while you work on the remote computer. The *ssh* client features many different command-line options, but can be simply used with the name of the remote computer, like this:

```
[andrew@laptop ~]$ ssh desktop
The authenticity of host 'desktop (192.168.2.3)' can't be established.
RSA key fingerprint is 91:7d:74:4b:1c:a1:96:06:ba:2f:d4:cf:78:44:ff:d7.
Are you sure you want to continue connecting (yes/no)? yes
```

The first time you connect with a remote computer using *ssh*, Linux displays the remote computer's encrypted identity key and asks you to verify the connection. After you type **yes** and press Enter, you're warned that the remote computer's identity (key) has been entered in a file named *known_hosts* under the *.ssh* directory in your home directory. You're also prompted to enter your password:

```
Warning: Permanently added 'desktop,192.168.2.3' (RSA) \
to the list of known hosts.
andrew@desktop's password: 
/usr/X11R6/bin/xauth:  creating new authority file /home/winky/.Xauthority
[andrew@desktop andrew]$
```

After entering your password, you can then work on the remote computer. Again, everything you enter on the keyboard in communication with the remote computer is encrypted. Use the *exit* or *logout* commands to exit your session and return to the shell on your computer.

> **CAUTION**
>
> The next remote access command, *telnet*, is shown as an example because it is included with most Linux distributions, but you shouldn't use it: *telnet* transmits your username and password in clear text across the network, posing a huge security risk for your system. Also, note that this service must be explicitly turned on and allowed on the remote computer (by editing the file named *telnet* under the */etc/xinetd.d* directory and then restarting *xinetd*; see the section "Starting and Stopping Services Manually" in Chapter 14 for more information on starting or restarting a system service).

The *telnet* command can be used, along with the name of a remote host or Internet Protocol (IP) address, to log in to a remote computer. For example, to log in to the host named *desktop* from the host named *laptop*,

```
[andrew@laptop andrew]$ telnet desktop
```

After you press Enter, you'll see some information presented by the remote computer, and you will then be prompted for your username on the remote system:

```
Trying 192.168.2.70...
Connected to desktop.andbhudson.co.uk (192.168.2.73).
Escape character is '^]'.

Linux 2.6.10-1.741_FC3 (desktop.andbhudson.co.uk) (15:43 on Friday, 4 February 2005)

login: andrew
```

After you type your username (*andrew* in this example), press Enter, and you'll be prompted for your password on the remote system:

```
Password:
Last login: Fri Feb  4 15:42:26 from 192.168.2.2
[andrew@desktop andrew]$
```

After you type your password and press Enter (your password is not echoed back), you'll be informed of the last time you logged in, and you can then work on the remote computer. Use the *exit* or *logout* commands to exit your session and return to the shell on your computer.

Although it is possible to use *telnet* to log in to a remote computer over a wired and wireless network, such use is not recommended, especially via the Internet. When you type your username and then press Enter and type your password, your username and password are transmitted without encryption over the network. Transmitting usernames and passwords over a network without encryption is a bad idea for obvious reasons. However, if you have a physically secure internal network not connected to the Internet, have firewall policies in place, and don't use wireless networking, there is nothing wrong with using *telnet*. In fact, the encryption overhead of using *ssh* can reduce network transmission rates in some cases.

> **NOTE**
>
> It is possible to use *telnet* securely over an encrypted Virtual Private Network (VPN), but that is beyond the scope of this chapter and book. Besides, why bother when you can use *SSH*?

## Changing Your User Information

Linux users are assigned a name, known as a *username*, by the *root* operator. One method of assigning usernames is to use one's first initial and last name in lowercase; for example, Bernice Hudson would have a username of *bhudson*. Each user must also have a password, which is used with the username either at a graphical or text-based login.
