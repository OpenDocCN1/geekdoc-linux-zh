If your modem was not automatically detected and the /dev/modem link configured, it is possible that you have a software modem, also known as a Winmodem or HSF modem (refer to the earlier note).

Set the baud rate (**38400** in the default case) to the desired connection speed—most likely 115200 or 57600. When finished, save the file.

Next, use the `chmod` command to make these scripts executable, like this:

```
# chmod +x /etc/ppp/ppp-o*
```

To debug or check the progress of your modem connection, dialing, and connection to your ISP, monitor the syslog messages by using the `tail` command with its -f "loop-forever" option, as follows:

```
# tail -f /var/log/messages
```

To connect to your ISP, run the ppp- script:

```
# /etc/ppp/ppp-on
```

Use the `ppp-off` script to stop the PPP connection, like so:

```
# /etc/ppp/ppp-off
```

You can also move the ppp-on and ppp-off scripts to a recognized $PATH, such as /usr/local/bin. Enabling use of these scripts by normal users will entail changing permissions of the serial port and other files (which can be a security problem because unauthorized users can access it).

# TIP

If your modem is installed and working, you can access it with a terminal program such as minicom, which usually is not installed by default. After you install it using yum or from source code, start it the first time with the -s argument to configure it:

```
$ minicom -s
```

Set the serial port to that of your modem, and then save the configuration. You can then use minicom to communicate with your modem by using the AT command to set and see its responses.

If you do not want to go to that trouble, you can use the `echo` command to send commands to the modem, but the modem won't be capable of responding to you. For example, the `AT&W` command can be sent as follows:

```
# echo "AT&W" > /dev/modem
```