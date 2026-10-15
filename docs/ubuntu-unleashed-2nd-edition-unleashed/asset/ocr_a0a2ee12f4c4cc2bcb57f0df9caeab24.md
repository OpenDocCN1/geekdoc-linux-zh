After saving your changes, restart gpm like so:

```
$ sudo /etc/rc.d/init.d/gpm restart
```

Your mouse buttons will now be reversed!

You can change your keyboard layouts by using the loadkeys command. To use a different font for the console, try the setfont command. Ubuntu comes with nearly 150 different console fonts, which are found under the /lib/kbd/consolefonts directory.

> **NOTE**
> A text-based, dial-up login, also known as a shell account, looks much the same as a text-based login at a PC running Linux. Details about setting up Linux to answer the phone and provide a login prompt via a modem are in Chapter 18. Using dial-up access has some limitations, such as the inability to use virtual consoles. From a shell account, however, you can start programs in the background (using an ampersand, &), run programs after logging out with the nohup command, or use the screen command to simulate virtual terminals (an approach that works much like using virtual consoles). For more information on different shells included with Linux, see Chapter 15.

# Logging Out

Use the exit or logout commands to exit your session. Type the command and press Enter. You will then be returned to the login prompt. If you use virtual consoles, remember to exit each console before leaving your PC. (Otherwise, someone could easily sit down and use your account.)

# Logging In and Out from a Remote Computer

Although you can happily log in on your computer, an act known as a local log in, you can also log in to your computer via a network connection from a remote computer. Linux-based operating systems provide a number of remote access commands you can use to log in to other computers on your local area network (LAN), wide area network (WAN), or the Internet. Note that not only must you have an account on the remote computer, but the remote computer must be configured to support remote logins—otherwise, you won’t be able to log in.

> **NOTE**
> See Chapter 18 to see how to set up network interfaces with Linux to support remote network logins and Chapter 15 to see how to start remote access services (such as sshd).