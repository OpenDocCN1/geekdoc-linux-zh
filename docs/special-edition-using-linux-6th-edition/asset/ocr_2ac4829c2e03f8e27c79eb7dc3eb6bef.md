**TABLE 24.3. CONTINUED**

| Option | Description |
|---|---|
| `persist` | Does not exit after connection termination, but tries to reestablish the link. Designed to provide a continuous connection. |
| `silent` | Sets `pppd` to not transmit any LCP packets until a valid LCP packet is received. |

The preceding options are only a few of the many options available for pppd. For the complete list of options, see the man page for pppd. An example of a working `/etc/ppp/options` file follows:

```
connect "/usr/sbin/chat -f /etc/ppp/chat-script"
/dev/modem 38400
crtscts
defaultroute
nodefaultroute
```

In the preceding options file, the first two lines are the most important. The first line indicates how pppd is to access the modem line. In this example, a chat script is called through the chat utility, the script discussed in the preceding section. The second line defines what device to use. In this example, the device `/dev/modem` is used, but it might just as easily have been `/dev/ttyS0` or `/dev/ttyS1`, depending on which serial port the modem is connected to.

> **Note:** You must either use the actual device name in the `/etc/ppp/options` file or create a symbolic link to it and use the symbolic link name. A symbolic link is recommended for use in the options files. This enables changes to modem port without necessary changes to the options file. It’s just a matter of changing the symbolic link.

The `/dev/modem` device is not created by default. It is only a symbolic link to the actual serial device to which the modem is connected. It can be created as follows:

```
# ln -s /dev/ttyS0 /dev/modem
```

The first COM port is usually `/dev/ttyS0` and the second COM port is usually `/dev/ttyS1`.

# CONFIGURING AUTHENTICATION FILES

Authentication to the PPP server takes place in one of several ways, the most common being manual, PAP, and CHAP (refer to Table 24.2). Manual authentication takes place by simply supplying a user ID and password to the PPP server. PAP and CHAP authentication require special files.

> **Note:** Your Internet service provider will only offer one method of authentication. You only need to configure your system according to the authentication method used by your provider.