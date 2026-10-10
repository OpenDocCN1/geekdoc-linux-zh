
- The netmask to use with your network.
- The broadcast address to use on your network.
- The IP address of the default gateway system (if your network has a gateway).
- The router for your connection.

## Configuring a Network Connection From the Desktop

![](img/e36b94f8548b09d00212238f073b11d9_386_0.png)

Network configuration is used not only for a network, but also for a cable or DSL internet connection. If you are an end-user, ask your system administrator or internet provider for the settings you need.

1. From the GNOME Control Center, select System > Network.

**Note**
If you are using the KDE desktop, type `/usr/bin/network-configlet-capplet` at the command line.

2. Enter a hostname for your machine.

3. Select one of the following:
   - No network configuration: Continue the install without setting up a network. If you want to add network support later, you can do so after the install.
   - Configure with DHCP: Network information is assigned automatically by the DHCP server. The DHCP hostname is assigned by an ISP to your machine. This setting is optional. In most cases, it can be ignored.
   - Use manual settings: Enter the settings needed for the network:
     - Domain name: The name of the machine on which you are installing Progeny Debian.
     - IP address: The address of the machine on which you are installing Progeny Debian.
     - Netmask: The bitmask that defines the part of the system’s network address that identifies the network.
     - Gateway: The address of the machine that is the default route to machines not on the network.
     - Name Servers: The address of the system that provide hostname lookup services to your system.

Note
Check with your system administrator or Internet service provider for the entries that you need.

4. If your network connection is through a *PCMCIA* or *Cardbus* network card, select the box beside *Main network device is removable*.

## Configuring a Network Connection From the Command Line

1. Logged in as root user, add your hostname to /etc/hostname.
2. Add your hostname and IP address to /etc/hosts.
3. Add at least your IP address, and netmask to /etc/init.d/network. You may need to add other information to enable your connection.
4. If necessary, add your nameserver to /etc/host.conf and /etc/resolv.conf.

## Configuring a Temporary Network Connection

You can use Linux commands to set up a temporary connection without editing files. This type of on-the-fly configuration is especially useful for testing configurations.

To setup a temporary connection:

1. Logged in as root user, type: `ifconfig DEVICE IPADDRESS NETMASK`.
2. Add the route. Type: `route add default gw ROUTE`.
3. If necessary, add your nameserver to /etc/resolv.conf.

If you log out, re-do the first two steps to re-create the temporary connection.

## Configuring a Dialup Internet Connection

A dialup connection uses a modem and an unmodified telephone line. A dialup connection is also known as a Point-to-Point Protocol (ppp) connection.

![](img/e36b94f8548b09d00212238f073b11d9_388_0.png)

### Warning
For greater security, use a regular user account for your connection. Never use the internet when logged in as root user.

1. At the command line, type `dpkg-reconfigure pppconf`. The `pppconf` tool opens.

![](img/e36b94f8548b09d00212238f073b11d9_389_0.png)

2. Select the Yes button to have your modem detected. A button is blue when selected.

If your modem is not connected, see “Troubleshooting a Dialup Connection,” page 388.

3. Enter the phone number that you use to connect to your Internet Service Provider. Then select the Yes button.

4. Enter the log in name for your internet account.

5. Enter the password for your internet account.

# Troubleshooting a Dialup Connection

If you are having trouble making a dial-up connection:

- Make sure that you are not trying to use a winmodem or host-based modem.
- Check the port to which your modem is connected. Usually, it will be on ttyS0 (COM1).
- Make sure that your modem is properly setup and turned on.
- To ensure that your system can find the modem, create a symbolic link between the serial port to the /dev/modem device. Type: `ln -s /dev/serialport /dev/modem`.

- Check the pppd man page for more options.

## Setting Up E-Mail

![](img/e36b94f8548b09d00212238f073b11d9_390_0.png)

Unless set to local only, e-mail requires a network or dialup connection. You can configure a network during the install process or after. A dialup connection is not part of the install program, but you can set up one after the install process.

If you need help with the choices on this screen, consult your system administrator or Internet service provider.

1. From the GNOME Control Center, select System > Electronic Mail.

> **Note**
>
> If you are using the KDE desktop, type `/usr/bin/mail-configlet-applet` at the command line.

2. Select the General mail setup. Choices are:
   - Internet Site: The same machine that originates the mail sends it and receives any incoming mail.
   - Internet with smarthost: A dedicated server delivers mail. This setting is often used when you are connecting to an Internet service provider.
   - Satellite system: No mail is delivered locally. Mail is delivered only through the smarthost.
   - Local only: E-mail can only be sent and received by users on the present machine.
   - No configuration: No e-mail is configured.

3. Enter the outgoing mail hostname. Consult your system administrator or ISP provider for the hostname needed.

4. Enter the incoming mail hostname. Consult your system administrator or ISP provider for the hostname needed.

5. Enter the SMTP relay host. Consult your system administrator or ISP provider for the hostname needed.

6. Check the appropriate box if you want a world-writable mail drop.

A world-writable mail drop allows users to receive mail directly, instead of only through your network's mail system. It is faster, but can be a security risk.

If in doubt, do not select world writable mail drop.

7. Check the appropriate box if you want to use “procmail” for local mail delivery.

Procmail lets you filter incoming messages and deliver them to folders other than your Inbox.

You can use other tools to filter, so, if in doubt, do not use procmail.

8. Configure the mail program you want to use.

## Directing E-Mail Using procmail

You can use procmail to arrange your e-mail so that messages from a source go into a particular directory.

1. In the GNOME Control Center, select the box beside Use "procmail" for local delivery on the System > Electronic Mail pane.
2. Create a text file called .procmailrc in your home directory. See “Lines in the .procmail File,” page 391.
3. If necessary, create the directory in which to filter mail. This directory can be one created and used by another mailreader.
4. Create a sub-directory in your home directory called .procmail to hold procmail files.
5. Create filters. Place each filter in a file called rc.FILTER in the .procmail directory. See “Filters for procmail,” page 392.
6. Create a file called .forward in your home directory. This file activates procmail when new mail arrives.

In the .forward file, enter:

```
"IFS='\| ' exec /usr/bin/procmail -f || exit 75 #user"
```

![](img/e36b94f8548b09d00212238f073b11d9_392_0.png)

> Note
>
> For examples of .procmail files and more ideas of what you can do with them, see the sample files in the /usr/share/docs/procmail/examples directory.

## Lines in the `.procmail` File

| Line | What It Does |
| :--- | :--- |
| PATH= /usr/bin | Defines the location of the utility. |
| MAILDIR=DIRECTORY | Defines the directory to which mail is sent. If this directory does not already exist, be sure to create it. |
| PMDIR=~/HOME/.procmail | Defines the directory in which procmail files are stored. |
| LOGFILE=~/HOME/.procmail/log | Defines the procmail log file. |
| DEFAULT=MAILDIRECTORY/DIRECTORY | Defines the default location for mail. This setting is overridden by any INCLUDEDRC line. |
| INCLUDEDRC=~/HOME/.procmail/rc.FILTER | Defines a sender whose mail you want to filter. Include one line for each sender. |

## Filters for procmail

| Filter | What It Does |
| :--- | :--- |
| :0:\n^Sender: *KEYWORD\nDIRECTORY | Sends a message that contains the keyword to the specified directory. |
