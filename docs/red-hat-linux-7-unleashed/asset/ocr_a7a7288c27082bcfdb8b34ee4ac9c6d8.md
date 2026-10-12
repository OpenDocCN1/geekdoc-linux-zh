Linux uses CSLIP by default for most SLIP lines because it packs more information in the same space as SLIP. If your ISP or whoever you are connecting to does not support CSLIP, you need to force Linux to use only SLIP. You can do this on the slattach line:

```
# slattach -p slip /dev/ttyS0 &
```

This tells slattach to use only the SLIP protocol. Other valid arguments after the -p option are cslip (for CSLIP), adaptive (which adjusts to whatever is at the other end of the connection), ppp, and kiss (for packet radio).

Now that the SLIP device has been created, you need to tell the Linux kernel about it, using the ifconfig program for setting up the dummy interface. The ifconfig line that establishes the interface requires the name of the remote system:

```
ifconfig sl0 mymachine-slip pointopoint remoteremote machine
```

sl0 is the name of the interface (/dev/s10 in this case); mymachine-slip is the local name of the SLIP interface (you should substitute your machine's name, such as merlin-slip or darkstar-slip); pointopoint tells ifconfig the interface is a point-to-point connection (not to be confused with PPP); and remoteremote machine is the name of the machine at the other end of the connection. For example, if the remote machine's name is darkstar and your machine's name is dogbert, the ifconfig command looks like this:

```
ifconfig sl0 dogbert-slip pointopoint darkstar
```

The next step is to issue the route command to add the route to the remote machine to the system databases. The syntax is the same as when you set up the dummy interface:

```
route add darkstar
```

In this case, you are adding a route to the remote machine called darkstar. You should substitute whatever the remote machine is called.

# **Note**

Many ISPs don't tell you their remote machine's names. That's fine because these machine names are only placeholders; the important information needed is the IP addresses. Although not recommended, you can substitute any name you want that identifies the other end of the connection, as long as the name is defined in your /etc/hosts file. However, the associated IP address must be correct.