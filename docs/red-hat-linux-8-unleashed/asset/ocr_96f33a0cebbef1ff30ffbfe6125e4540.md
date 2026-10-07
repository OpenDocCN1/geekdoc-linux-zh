# Configuring a Dial-in PPP Server

+   - Always make certain that everything is plugged in. Check again—and again.

+   - If the modem works in Windows, but not in Linux, it's probably a software modem
o matter what it said on the box.

+   - If everything just stops working (and you don't see smoke), it's probably a glitch at
the ISP or the telephone company. Take a break and give them some time to fix it.

+   - Never configure a network connection when you had too little sleep or too
much caffeine; you'll just have to redo it to tomorrow.

# Configuring a Dial-in PPP Server

If you want to access your high-speed Internet connection when you are away from home,
a simple dial-up PPP service can be quickly configured on your Red Hat Linux system by
figuring Linux to answer a call from a remote modem and start PPP. This is handy if
you have high-speed access at home and need to use it while you're on the road. For
example, our DSL connection is made through the telephone lines to home. If we are
at our summer vacation home, that DSL connection is not available to us. With a dial-in
ser the modem in our laptop to dial home and the dial-up server connects to us
the Internet; it like a private ISP. Not everyone will want to configure a dial-in PPP server
to do this, but does it ctypes the kind of power that dial-in offers a user.

You'll need a second phone line (for convenience), a serial port, and an attached modem.
The modem must be set to answer incoming calls using the AT commands specific to the
modem you are using (consult its manual), and with the configuration saved using the
AT&W modem command. A line-monitoring application such as as, getty, or mtty is
tused to watch the serial port by editing an entry in the system's initialization table
/etc/inittab. You then create a special user account and script to configure Red Hat
Linux to automatically start the ppt daemon and PPP service after a user logs in.

> NOTE\If your modem is installed and working, you can access it using a terminal program like minicom,\which usually isn't installed by default. After you install the .rpm file or from source,
start the first time with the -s argument to configure it:

```
$ minicom -s
```

Set the serial port to that of modem, and then set the configuration. You can use the
minicom to communicate with your modem using the AT command set and see its responses.

If you don't want to go to that trouble, you can use the echo command to send commands
the modem, but the modem won't be respond to you. For example, the AT&W command
be sent as follows:

```
# echo "AT&W" > /dev/modem
```