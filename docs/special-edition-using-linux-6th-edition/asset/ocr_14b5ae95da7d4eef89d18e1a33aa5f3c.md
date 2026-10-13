category 3 or cross-connect (cross-over) cables, which would allow you to connect Ethernet card to Ethernet card). You might also want to make sure that if your hub has an uplink port that you’re not using that for one of your computers.

*I installed an ISA NIC and I just can’t seem to get it working. What could be wrong?*

First, make sure in the BIOS setup you have turned off PNP OS. Also, make sure your Ethernet card is set up manually. If it’s set for PNP, you’ll need to use pnpdump to create an `/etc/isapnp.conf` file, and then configure the file and run `isapnp /etc/isapnp.conf` to configure the card. Usually it’s just easier to simply set the IRQ and I/O port using the jumpers on the card. Ensuring that you have your NIC set to unused values for the IRQ and I/O settings (`cat /proc/interrupts` and `cat /proc/ioports`), should help you find unused settings.

*I’m having lots of problems trying to connect with my modem to my ISP.*

I suggest you look at Chapter 24, “Connecting to an ISP,” for help with this.

![](bbox=[0.934, 0.217, 1.0, 0.337])