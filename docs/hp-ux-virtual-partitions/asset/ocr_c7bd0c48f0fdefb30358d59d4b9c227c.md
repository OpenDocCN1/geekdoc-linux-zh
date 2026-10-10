# # Virtual Partitions and LAN

The LAN cards on your system are also easy to identify with **ioscan**. To see only the listing of LAN cards on a system, we would issue the following command:

```
# ioscan -f | grep lan
lan   0  0/0/0/0        btl an5   CLAIMED   INTERFACE   PCI Ethernet (10110019)
    ~ 1                btl an5   CLAIMED   INTERFACE   PCI A5230A/B5559BA
                                  PCI 10/100Base-TX Addon
lan   3  0/5/0/4/0      btl an   CLAIMED   INTERFACE   PCI 10/100Base-TX 4 port
lan   4  0/5/0/5/0      btl an   CLAIMED   INTERFACE   HP A5506B
                                  PCI 10/100Base-TX 4 port
lan   5  0/5/0/6/0      btl an   CLAIMED   INTERFACE   HP A5506B
                                  PCI 10/100Base-TX 4 port
lan   6  0/5/0/7/0      btl an   CLAIMED   INTERFACE   HP A5506B
                                  PCI 10/100Base-TX 4 port
lan   2  1/2/0/0        btl an5   CLAIMED   INTERFACE   PCI A5230A/B5559BA
                                  PCI 10/100Base-TX Addon
#
```

This system has seven LAN interfaces. It has the built-in LAN interface, two add-on LAN cards, and a four-port card. Although this system was not used in our earlier example, I wanted to show a listing of a system with a variety of LAN interfaces present.

Going back to our earlier example, our system has three LAN interfaces as shown in the following **ioscan** listing:

```
cvhdcn3:/ # ioscan -f | grep lan
lan   0  0/0/0/0        btl an   CLAIMED   INTERFACE   HP PCI 10/100Ba
se-TX Core
lan   1  0/10/0/0       btl an   CLAIMED   INTERFACE   HP AS230A/B5509
BA PCI 10/100Base-TX Addon
lan   2  0/12/0/0       btl an   CLAIMED   INTERFACE   HP AS230A/B5509
BA PCI 10/100Base-TX Addon
cvhdcn3:/> #
```

The LAN card at 0/0 has been assigned to *cable1*, and the card at 0/10 has been assigned to *cable2*, as shown in the following **vparstatus -v** listing:

```
# vparstatus -v

[Virtaul Partition Details]
Name:     cable1
State:    Up
Attributes: Dynamic,Manual
```

![](bbox=[0.85, 0.83, 0.94, 0.94])