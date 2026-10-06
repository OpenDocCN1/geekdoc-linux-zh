# Attaching Cables and Adapters

After hardware is mounted, you can begin plugging in various cables and adapters to attach it to power sources, network devices, disk arrays, and any other equipment you may have. You should tighten any screws that fasten adapters to the ports on your hardware; an insecure connection on any port could result in an unreliable signal causing random data loss and errors.

# Bending Pins

You should be especially careful when plugging in cables and adapters with very thin pins, like those on most SCSI cables. Even the slightest offset from the hole can cause a pin to bend or break, ruining the cable itself. You may also fix bent pins, but you run the risk of worsening the problem by breaking it or bending other pins.

You will also want to use this to label your cables. Each label should indicate the type of cable and the hardware at either end of the connection, including interface names. For example, a 5 cable connecting the eth0 network interface on a Linux server called apple to a 100Mb switch read:
eth0/100 Mb Ethernet

# Real-World Example: Using Colored Cables

Some organizations use colored cables to indicate their purpose. One such company used category 6 cable for its network connectivity, digital phone lines, and analog phone lines. The company used red, white, and blue cables to differentiate each function so administrators could clearly see what kind of traffic was flowing over each cable.

# Premature Power On

Make sure the power switch is turned off before plugging in a power cable; otherwise, the machine may power on before you are ready.

Special care should be taken with power cables. As mentioned in Chapter 2, you should separate power cables from other types of cables; the electromagnetic interference from power cables can introduce errors into the signals on other cables.

# Testing Your Hardware

After your hardware has been racked and connected to other devices, you should test to see that everything powers on correctly. For most systems, this is as simple as flipping the switch and verifying that any fans or LED indicators are activated; you haven't installed any software yet, so there is not much else you can test for this point.