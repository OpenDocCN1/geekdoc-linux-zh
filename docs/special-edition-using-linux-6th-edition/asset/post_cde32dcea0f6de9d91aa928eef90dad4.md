
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

> **Note:** You must either use the actual device name in the `/etc/ppp/options` file or create a symbolic link to it and use the symbolic link name. A symbolic link is recommended for use in the options files. This enables changes to the modem port without necessary changes to the options file. It’s just a matter of changing the symbolic link.

The `/dev/modem` device is not created by default. It is only a symbolic link to the actual serial device to which the modem is connected. It can be created as follows:

```
# ln -s /dev/ttyS0 /dev/modem
```

The first COM port is usually `/dev/ttyS0` and the second COM port is usually `/dev/ttyS1`.

## CONFIGURING AUTHENTICATION FILES

Authentication to the PPP server takes place in one of several ways, the most common being manual, PAP, and CHAP (refer to Table 24.2). Manual authentication takes place by simply supplying a user ID and password to the PPP server. PAP and CHAP authentication require special files.

> **Note:** Your Internet service provider will only offer one method of authentication. You only need to configure your system according to the authentication method used by your provider.

### MANUAL AUTHENTICATION

Manual authentication of a PPP client to a PPP server is done by logging on to the PPP server and starting pppd. This method is completely dependent on the chat script written to handle the interaction between the client and the server. No other configuration files are required. It works much like the normal process of logging on: The system presents a login prompt, you enter your user ID, the system responds with a password prompt, and you enter your password. The trick is to automate this process by configuring a chat script of expect and send strings. An example of this type of script follows:

```
ABORT     BUSY
ABORT     "NO CARRIER"
ABORT     "NO DIALTONE"
""        ATZ
OK        "AT S0=0"
OK        ATDT5551386
CONNECT   ""
ogin: \d\q'mylogin'
ssword: \q'mypassword'
""        \d\c
```

The first part of the chat script remains the same. The last three lines represent the automated login steps. This is how it works: The chat script waits for the ogin: string, which is the expect string. When this is detected, the string mylogin (of course this is changed to the actual User ID) is sent back to the PPP Server. The same holds true with the password prompt and actual password. Notice that the expect string does not have to be a complete string. To avoid issues of whether or not the prompt is capitalized and so on, you can just place a unique portion of the string in the chat script. The final line provides a delay just in case it takes your ISP a few seconds to respond. The `\d` specifies a one second delay. The `\q` tells chat not to send the following string to syslog; send `????` instead. The `\c` in the last line says not to send a carriage return. See the chat man page for a list of all the escape codes chat understands.

### PAP AUTHENTICATION

PAP authentication is done by including the necessary information in the `/etc/ppp/pap-secrets` file. This means that you do not have to create the chat script to look for a login prompt and send the user ID and password information; this is all handled by the PAP authentication protocol. Simply add the user ID and password to this file as follows:

```
# Client       Server       Secret
  mylogin        *           mypassword
```

Of course, mylogin and mypassword are changed to your user ID and password.

> **Note:** With both PAP and CHAP authentication methods, you must add an entry to the `/etc/ppp/options` file as follows:
>
> `name mylogin`
>
> `mylogin` is your actual user ID.

### CHAP AUTHENTICATION

CHAP authentication works in much the same way as PAP authentication. The information to enable CHAP authentication is stored in the `/etc/ppp/chap-secrets` file. The format of the chap-secrets file is described in the comments included at the beginning of this chapter as follows:

```text
# Secrets for authentication using CHAP
# client        server        secret        IP addresses
```

According to the AT&T WorldNet Users Reference Desk Web site (`http://204.127.237.208/wurd/software/dialers/linux.html`), the chap-secrets file needs to be set as follows for authenticating an AT&T WorldNet account:

```text
# Secrets for authentication using CHAP
# client                 server  secret     IP addresses
99999999@worldnet.att.net  *     "password"  *
```

The previous setting, however, is only for AT&T Worldnet. The actual CHAP implementation requires two lines with 3–4 entries per line for each client-server connection. Each line has a client name, a server name, a secret for authentication, and optionally, an IP address to which the server must correspond.

The first of the two lines lists the name of the local system, the name of the remote system, and then a secret. The second line is similar, but the local and remote hosts are swapped. The secret is usually also different. The IPs, if present, are used to enhance the security of this mode, because the IP must correspond to the server. When the hosts send the secret, it is first encrypted. When a challenge arrives from the remote host, the local host encrypts the secret and compares it to what it received. If your secret is a phrase containing whitespace, it must be quoted.

## CONFIGURING OTHER REQUIRED NETWORK COMPONENTS

In addition to the necessary PPP configuration files that you need to make operational, you’ll need to configure a couple of other files to have your Internet connection work correctly. First, the `/etc/hosts` file needs to contain an entry identifying your host name and IP address. If this machine is a standalone system (not connected to a network), add a line to your `/etc/hosts` file as follows:

```text
0.0.0.0    yourmachine.yourdomain.com yourmachine
```

The IP address is set dynamically when you connect to your ISP using PPP. Of course, you’ll want to set your machine name and domain to something more creative than `yourmachine.yourdomain.com`.

Also, a key piece of information gathered from your ISP is the IP address of the Domain Name Server (DNS). Set this value in the `/etc/resolv.conf` file as follows:

```text
# possible entries are:
#
#       domain <domain>                  Local domain name. If not present, the
#                                        gethostbyname syscall is used to
#                                        determine the local domain name.
#
#    search <list_of_domains>       Search list for hostname lookup.
#                                     The search list is normally determined
#                                     from the local domain name but it
#                                     can be set to a list of domains.
#
#    nameserver <ip_addr>             Define which server to contact
#                                     for DNS lookups. If there are
#                                     multiple nameserver lines (max=3),
#                                     they are queried in the listed order.
#
#
#domain mydomain.com
nameserver 207.179.18.1
```

## RUNNING /usr/sbin/pppd

After everything is configured, you can try a PPP connection by simply running the pppd utility as follows:

```
# /usr/sbin/pppd
```

The pppd utility offers several options, each of which is described in the man page for pppd. A common option is the detach option. This option starts pppd in the foreground (a non-background job), which allows terminating the PPP session with a keyboard sequence (Ctrl+C). Starting pppd with this option can be done as follows:

```
# /usr/sbin/pppd -detach
```

To terminate the PPP process without using the detach option, you must know the process ID. However, the process ID is stored in the `/var/run` directory, or you can find it by examining the process table. You can check the status of a successful PPP connection by checking the available network interfaces with the ifconfig utility.

When you want to kill this pppd process, you can use this command line:

```
kill `pidof pppd`
```

## TROUBLESHOOTING THE CONNECTION

You can troubleshoot the PPP connection process by adding a couple of options in the `/etc/ppp/options` file. First of all, the chat utility produces more verbose output if you add the `-v` option as shown in the following options file:

```
connect "/usr/sbin/chat -v -f /etc/ppp/chat-script"
/dev/modem 38400
crtscts
defaultroute
noipdefault
```

The second method of capturing more information about the PPP connection is to add debug statements to the `/etc/ppp/options` file as follows:

```
connect "/usr/sbin/chat -v -f /etc/ppp/chat-script"
/dev/modem 38400
crtscts
defaultroute
```
