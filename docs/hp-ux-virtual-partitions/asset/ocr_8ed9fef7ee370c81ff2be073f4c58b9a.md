```
```
Name    Mtu   Network           Address       Ipkts Ierrs Opts  Cerrs Coll
lanl    1500  172.16.14.0       172.16.14.44  3619  0     1545  0     2
lo0     4136  127.0.0.0         127.0.0.1     916   0     916   0     0
```

```
# ! lanscan
Hardware Station     Crd Idw Net-Interface IM      MAC                 HP-DLPI DLPI
Fach  Address        0/0/8 State Name*TPA          ID Type             Support BITS
C/10/0/0  0x0010680053658  1   UP  lanl snapi        1 ETHER          Yes     119
s
```
```

This output shows that lanl is the network interface devoted to vPar cable2 on this server. The lanscan output shows that this interface has a hardware path of 0/0/10/0/0. The LBA of 0/0/10/0/0 was configured as a component of the vPar when it was created with -a 10:0/10/0/10. Unlike the LAN interface on the Core I/O card that was an implied component, this LAN interface is in a separate PCI slot and LBA and therefore had to be specified explicitly when the vPar was created.

Running lanadmin on cablel produces more detailed output related to lan0, as shown in the following listing:

```
```
# lanadmin

LOCAL AREA NETWORK ONLINE ADMINISTRATION, Version 1.0
          Mon, Oct 15, 2001  14:41:23

     Copyright 1994 Hewlett-Packard Company.
             All rights are reserved.

Test Selection mode.

        lan     = LAN Interface Administration
        menu    = Display this menu
        quit    = Terminate the Administration
        tetera  = Do not display command menu
        verbose = Display command menu

Enter command: lan

LAN Interface test mode. LAN Interface PPA Number = 0

        clear   = Clear statistics registers
        display = Display LAN Interface status and statistics registers
        end     = End LAN Interface Administration, return to Test Selection
        menu    = Display this menu
        ppa     = PPA Number of the LAN Interface
        quit    = Terminate the Administration, return to shell
        reset   = Reset LAN Interface to execute its selftest
        specific = Go to Driver specific menu

Enter command: d

                    LAN INTERFACE STATUS DISPLAY
                    Mon, Oct 15, 2001  14:42:33

PPA Number         =      0
Description        =  lan0  HP PCI 10/100Base-TX Core [100BASE-TX,HD, AUTO, TT=1500
Type (value)       =   ethernet-commacd(6)
MTU Size           =   1500
Speed              =   100000000
Station Address    =   0x360056f8ba
```
```