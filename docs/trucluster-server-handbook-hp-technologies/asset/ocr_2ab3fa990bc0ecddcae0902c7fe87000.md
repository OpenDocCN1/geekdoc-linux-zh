In this example, we use a gigabit Ethernet LAN card as a cluster interconnect, and we must now tell the software the type of device that it is. In this case, the device is “alt0”. For the purposes of our example as we are only using one Ethernet device as a cluster interconnect, we choose not to put this Ethernet device into a NetRAIN set. For more information on NetRAIN and the benefits of using NetRAIN, please refer to Chapters 9 and 12.

```
The physical cluster interconnect interface device is the name of the physical device(s) which will be used for low level cluster communications. Examples of the physical cluster interconnect interface device name are: tu0, eo0, and nr0.

Enter the physical cluster interconnect device name(s) []: alt0
Would you like to place this Ethernet device into a NetRAIN set? [yes]: no
Checking physical cluster interconnect device name(s): alt0

You entered 'alt0' as your physical cluster interconnect interface device name(s). Is this correct? [yes]:
```

Now that the software knows what the physical cluster interconnect device is, we need the physical cluster interconnect IP name and IP address. The physical cluster interconnect IP name is created from the word “member” and appended with the member ID and “-icsctcp0”. In our example, this would be member1-icsctcp0. This is done automatically for us.

+   The default physical cluster interconnect IP address is created by appending the member ID “1” to the default private subnet 10.1.0.0. Again, we decide to accept this default for the sake of simplicity as it is reserved and address per RFC 1918 (private and non-routable) and it is a good choice to meet our needs in creating a cluster.

```
The physical cluster interconnect IP name 'member1-icsctcp0' was formed by appending '-icsctcp0' to the word 'member' and the member ID.
Checking physical cluster interconnect IP name: member1-icsctcp0

The physical cluster interconnect IP address '10.1.0.1' was created by replacing the last byte of the default cluster interconnect network address '10.1.0.0' with the previously chosen member ID '1'.
To use this default value, press Return at the prompt.

The cluster physical interconnect IP address is the IP address associated with the physical cluster interconnect IP name. (192.168.168.1 is an example of an IP address.)

Enter the IP address for the physical cluster interconnect [10.1.0.1]:
Checking physical cluster interconnect IP address: 10.1.0.1

You entered '10.1.0.1' as the IP address for the physical cluster interconnect.
Is this address correct? [yes]:
```

For more information on configuring an Ethernet LAN card as a cluster interconnect, please see section 4.4.2.