
For this example, assume that your SuSE Linux has only one modem to which you're dialing in using terminal login.

### The `/etc/ppp/options` ttySxx Files

Each serial port on your SuSE Linux can have its own configuration file. For example, you can have a `/etc/ppp/options.modem` in which `modem` is a symbolic link to your modem serial port. If you have a multi-port board—a board that has more than one serial board designed for ISPs—each serial port can have its own options file, too. This configuration is integral to assigning IPs to users dialing in to this serial port.

The following is an example of a `/etc/ppp/options.modem` that will assign the caller an IP of `192.168.1.2` while assigning SuSE Linux an IP of `192.168.1.1`:

```
# server  : client
192.168.1.1:192.168.1.2
```

If you have more than one modem or a multi-port board, you can assign IPs to callers by modifying the files. You can accomplish this using the following example, which assumes you are on a class C network with IPs starting from `208.159.7.0` to `208.159.7.255`:

```
/etc/options/ttyC0
# server  : client
208.159.7.100:208.159.7.101
```

```
/etc/options/ttyC1
# server  : client
208.159.7.100:208.159.7.102
```

```
/etc/options/ttyC2
# server  : client
208.159.7.100:208.159.7.103
```

```
/etc/options/ttyC3
# server  : client
208.159.7.100:208.159.7.104
```

## A Dial-In Server Example

In this example, you will learn how to apply the configurations discussed in the previous sections. The following are assumed:

- The SuSE Linux server is connected over a LAN—SuSE Linux has the IP `192.168.1.24` over this LAN. The DNS servers of the LAN are `192.168.1.1` and `192.168.1.2`.
- The SuSE Linux server has only one modem, which has a symbolic link `/dev/modem` that points to the correct serial port.—You use this modem to dial to the Internet, and now you want to use it to dial in. The phone line to which SuSE Linux is connected supports caller ID, as does the modem.
- You will be connecting to SuSE Linux using Windows 9x—Throughout this example, the machine dialing in and its OS will be called the client. You will be dialing in to this server from the following number: `4186813`. All other numbers will be disallowed.

Your goal is to contact the SuSE Linux server, log in to it, and view shares of the LAN on your Windows 9x Network Neighborhood.

The following steps are required to perform such an operation:

1. Set up Samba on your SuSE Linux server. This is important if you want to enable your clients to see the Windows shares on the LAN. Check whether your SuSE Linux server can see the shares.
2. Set up the workgroup in your Windows 9x to be the same workgroup as in your LAN. This step and the previous one are discussed in more detail in Chapter 15, "Connectivity with Windows Through Samba."

After you have set up these prerequisites, you can move on to configuring the dial-in facility.

## The Configuration for the Simple Dial-In Server

All the settings in the following section must be performed as root.

Add the following entry in the `/etc/inittab`:

```
mo:23:respawn:/usr/sbin/mgetty -s 38400 modem
```

After you have added the entry, issue the following command:

```
bash#kill -1 1
```

Then, add the following lines to the `/etc/mgetty+sendfax/mgetty.config` file:

```
speed 38400    #set the speed to 38400 for all modems
rings 3        #answer after the third ring
port modem     #modem on port /dev/modem
```

Check whether your `/etc/mgetty+sendfax/login.config` file has the following entry. Because it is a default, it's not important that the file has this entry; however, you should make sure that it is not overridden:

```
*       -       /bin/login @
```

Add the following lines to your `/etc/mgetty+sendfax/dialin.config`:

```
#disallow all numbers
!all
#allow the following numbers
4186813
```

Next, add the following lines to the `/etc/ppp/options` file:

```
ms-dns 192.168.1.1
ms-dns 192.168.1.2
modem
proxyarp
-detach
lock
```
