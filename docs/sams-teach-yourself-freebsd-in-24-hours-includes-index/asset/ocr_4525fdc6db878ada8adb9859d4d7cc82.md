When you have finished editing the /etc/resolv.conf file, you are ready to configure the connection. FreeBSD can connect to the Internet through a dial-up connection in two ways. The method that we will cover in this book is known as kernel PPP. It is slightly more efficient than the alternative, which is known as user PPP.

# Configuring the Options File for Kernel PPP

Most of the configuration for kernel PPP is done in the file /etc/ppp/options. Here is what a sample file might look like:

```
/dev/cuaa0 115200
crtscts
modem
connect "/usr/sbin/chat -f /etc/ppp/chat.script"
noipdefault
silent
domain myisp.com
defaultroute
user foobar
name foobar
```

Here is what each line means.

/dev/cuaa0 115200—This line indicates the device that your modem is on. You should have figured this out back when you gathered the information about your modem. In this case, as we pointed out earlier, cua a0 corresponds to COM1 in Windows. The second part of the line (115200) indicates the serial communication rate of the computer with the modem. Unless you have a very old system, 115200 should probably work fine. If you encounter weird problems, you might try reducing this to 57600.

crtscts—This line turns on hardware flow control for the modem. Hardware flow control is required in order for high speed communication to work reliably; this line is therefore required.

modem—This line tells FreeBSD that it should use the modem control lines.

connect "/usr/sbin/chat -f /etc/ppp/chat.script"—This line specifies the "modem script" to run when connecting. It calls the chat program, which is a simple way for FreeBSD to run to communicate with the modem. The second part of the line (/etc/ppp/chat.script) tells the chat program the name of the modem script that it should read and execute. We haven't created this script yet, but it is what will contain the phone number for the modem to dial, as well as other options.

noipdefault—This line means that your ISP has not assigned you a static IP address and that you are using a dynamic IP address. Most dial-up users will have a dynamic