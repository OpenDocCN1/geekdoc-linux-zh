/dev/ttyS2, for example, which becomes /dev/s10. If more than one SLIP port is created, they are numbered increasingly as /dev/s11, /dev/s12, and so on. Linux usually supports up to eight or more SLIP lines, but it is unlikely you will need this many.

Linux uses CSLIP by default for most SLIP lines because it packs more information in the same space as SLIP. If your ISP or whoever you are connecting to does not support CSLIP, you can force Linux to use only SLIP. You can do this on the scratch line:

```
# slattach -p slip /dev/ttyS0 &
```

This slattach tells you to use the SLIP protocol. Other valid arguments after the -p option are cslip (for CSL), adaptive (which adjusts to whatever is at the other end of the connection), slip6 (and older 6-bit version of SLIP).

Now that the SLIP device has been created, you need to tell the Linux kernel about it, using the ifconfig program for setting up the dummy interface. The ifconfig line that establishes the interface requires the name of the remote system:

```
ifconfig s0 mymachine-slip pointoint remotemachine
```

s0 is the name of the interface (/dev/s10 in this case); mymachine-slip is the local name of the SLIP interface (you should substitute your machine's name, such as merlin-slip or darkstar-slip); pointoint tells ifconfig the interface is a point-to-point connection (not to be confused with PPP) and remotemachine is the name of the machine at the other end of the connection. For example, if the remote machine's name is darkstar and your machine's name is dogbert, the ifconfig command looks like this:

```
ifconfig s0 dogbert-slip pointoint darkstar
```

The next step is to issue the route command to add the route to the remote machine to the system databases. The syntax is the same as you set up the dummy interface:

```
route add darkstar
```

In this case, you are adding a route to the remote machine called darkstar. You should substitute whatever the remote machine is called.

> Note
Many ISPs don't tell you their remote machines' names. That's fine, because these machine names are only placeholders. You can substitute any name you want that identifies the other end of the connection.