
# Internet Connections
CHAPTER 17

chat this script tells chat the following: Expect nothing from the modem to start (the two quotation marks), the string ATZ, and wait for the reply OK. After OK is received, chat sends the string ADDT2370400 dial out to the ISP's number. When a CONNECT string is received from the modem, sending nothing and wait for the string login; from the ISP. (This covers all the types such as login and Login). After getting login;, send the login and wait for word (the end of password) and send the password quite. After, that terminates and handles control over PPP.

Along with you, the ppp daemon, also installed in the /usr/sbin directory. If pppd is installed, you can find a ppp directory under the /etc directory containing some or all of the following:

```
# ls /etc/ppp
auth-down  ioptions ip-up      peers
auth-up    options resolv.conf
chap-secrets ip-down   pap-secrets resolv.prev
```

Manually creating PPP scripts is one way to set up a PPP user account, but you'll find the job lot easier using software tools with SuSE Linux. You'll need to copy the files ppp-on, ppp-off, and redialer from /usr/doc/packages/inetcfg/ppp2 directory into the /etc/ppp directory:

```
# cp /usr/doc/packages/inetcfg/ppp2/* /etc/ppp
```

These script files are:

- ppp-on Contains your ISP's phone number, your username and password, and modem options (which the baud)
- ppp-off A utility script that kills the interface and PPP connection
- redialer A PPP chat script

To set up these scripts, log in as the root operator and edit the file ppp-on in the /etc/ppp directory like this:

```
# pico -w /etc/ppp/ppp-on
```

First, look for the lines defining Internet Protocol, or IP addresses, as shown in the following:

```
LOCAL_IP=0.0.0.0      Local IP address if known. Dynamic = 0.0.0.0
REMOTE_IP=0.0.0.0     Remote IP address if desired. Normally 0.0.0.0
DEVICE=/dev/modem
```

![](img/cbac72550c7126a22162e94d91a0c360_554_0.png)

The series of zeroes (0) in the LOCAL and REMOTE entries indicate that your IP address is assigned dynamically and may change every time you log in. If you are assigned a static, or permanent IP address, you'll need to change the LOCAL_IP to match the IP given to you by your ISP. Change the DEVICE= entry, if needed, to point to the correct serial port (not required if you used vast to create /dev/modem).

Next, scroll through the file and set the proper baud rate to match your modem’s capabilities. These modem options will be used by chat when dialing out to connect to your ISP. For example, if you connect at 57600 baud, look for a line that begins

```
PPP_FLAGS=*38400 mru 1500 modem debug ...
```

and change the 38400 setting to

```
PPP_FLAGS=*57600 mru 1500 modem debug ...
```

Save the file and make it executable with the chmod command:

```
# chmod +x /etc/ppp/ppp-on
```

Next, open the file named redialer with your text editor. You'll need to enter one or more phone numbers, along with account information to log into your ISP. First, look for the following lines:

# This is a list of telephone numbers.

```
PHONE1=3144730
PHONE2=31420920
PHONE3=31420988
PHONE4=39991099
numbers=4
```

```
############################################################
#
ACCOUNT=AliBaba
PASSWORD=OpenSesame
```

The list of phone numbers provides alternative numbers chat will use to call if a busy signal is received or if the connect fails. If you only have one phone number, replace the first phone number and change these entries to

# This is a list of telephone numbers.

```
PHONE1=3214887
PHONE2=31420920
PHONE3=31420988
PHONE4=39991099
numbers=4
```

In this example, note that the first phone number has changed, a pound sign (#) inserted in front of the other numbers, and the number= entry has changed to 1. Continue through the file and change the ACCOUNT= and PASSWORD= entries to the username and password assigned to your ISP:

```
ACCOUNT=fred
PASSWORD=pass
```

If you continue through the file, you'll see the following two lines:

```
OK                ATD
CONNECT
```

Note that the ATD command string will force pulse dialing for the connection by default. Since this could slow down, especially if you use long-distance, change this string to tone dialing unless you're one of the few people using pulse dialing:

```
OK                ATD
```

Note: Embedding phone numbers in chat strings or PPP scripts on your system may not be a good idea. But if you need to use pulse dialing, make sure that the dialer script is not readable. You can also use one or more commas (,) inside the ATDT dialing string to insert appropriate pauses in the dialing process to time the sequence correctly. Next, change the CONNECT string to a generic CONNECT string:

```
CONNECT
```

This will ensure that your modem will connect at any speed. Save the file and make it executable:

```
# chmod +x /etc/ppp/dialer
```

Next, the file ppp-off:

```
# chmod +x /etc/ppp/ppp-off
```

Finally, use your text editor to open the file options in the /etc/ppp directory:

```
# pico -w options
```

Look for the line

```
auth
```

and then comment out the line (if authentication is not required) with a pound sign (#):

```
#auth
```

If you do not have Ethernet networking set up, look for the line:

```
proxy
```

and comment it out as you did previously. Save the file and exit. To debug or check the progress of your modem connection, dialing, and connection to your ISP, go to a different virtual console, or open another X11 window and use the tail command with -f "loop forever" option:

```
# tail -f /var/log/messages
```

To try your connection, use the ppp-on command:

```
# /etc/ppp/ppp-on
Dialing attempt number: 1
Connection established
Serial connection established
Using interface ppp0
Connect: ppp0 <--> /dev/modem
...
local IP address 207.172.33.149
remote IP address 10.11.64.68
...
```

You're connected! You can then test the connection with the ping command or other Internet utilities.

If you see that a connection has started, but you are unable to ping any remote host, the problem could be that your system does not have access to a DNS server. You can fix this by putting a nameserver entry and IP address in your /etc/resolv.conf file:

```
nameserver ipaddress_of_ISP_DNS
```

To bring the connection down, use the ppp-off command:

```
# /etc/ppp/ppp-off
Terminating on signal 2.
Script /etc/ppp/ip-down started (pid 1691)
Connection terminated.
Connect time 13.0 minutes.
Sent 12695 bytes, received 190432 bytes.
Waiting for 1 child processes...
script /etc/ppp/ip-down, pid 1691
script /etc/ppp/ip-down finished (pid 1691), status = 0x0
```

As you can see, you'll also get some statistics about your connection and the status of the PPP connection.

# Configuring a PPP Connection with the YaST Command

As you know, the YaST command is an easy-to-use graphical system administration tool included with SuSE Linux. You can also yast on the command line to configure your PPP connection. Log in as root, and then start YaST. In the main YaST menu, select the System administration menu item and press Enter. In the pop-up menu that appears, scroll down to Network configuration, press Enter, and select the Configure PPP network menu item, as shown in Figure 17.1.

FIGURE 17.1
Use YaST's PPP configuration menu item to configure a PPP connection.

![](img/cbac72550c7126a22162e94d91a0c360_558_0.png)

This process will create a default PPP configuration file for use with the wdial command (which will be used to start your connection). This configuration file is named wdial.conf and is located under the /etc directory. Use the Tab key to select the Setup button (shown in Figure 17.1) and press Enter to begin your configuration. You'll then see the wdial configuration dialog box, as shown in Figure 17.2.

![](img/cbac72550c7126a22162e94d91a0c360_559_0.png)

The configuration dialog box shown in Figure 17.2 is used to set language preferences, create or change profiles, autodetect your modem, configure DNS for your connection, or run wdial to test the setup. You can also scroll down the list to read help and troubleshooting files, and after creating a configuration, save the settings to an alternate profile (handy when you must maintain multiple accounts on the same computer).

Scroll down to the Configure the Current Profile item and press Enter to begin your PPP configuration. You will see the dialog box shown in Figure 17.3.
