![](bbox=[0.0, 0.1, 1.0, 0.3])

# MakerSpace
Party Lights

# DMX with the Kunbus Revolution Pi Core 3+

The DMX protocol for controlling lighting technology has its roots in stage and event technology, but it can also be used in home automation. We show you how to control DMX devices with the Revolution Pi module. By Martin Mohr

In principle, digital multiplex (DMX) technology lets you control all DMX devices through a simple and robust bus. DMX uses the RS-485 specification (i.e., asynchronous serial transfer) for data transmission. The signal is transmitted over two lines simultaneously with inverted voltage levels (±5V).

This type of data transfer is resistant to external interference signals and theoretically allows line lengths of up to 1,200 meters. However, the data transmission rate decreases with increasing line length. Up to a distance of 10 meters, a maximum data rate of 10Mbps can be achieved over RS-485.

DMX works with a data rate of 250kbps by default; a DMX network is built of strings. One string can contain up to 32 DMX receivers. More receivers require the use of a repeater to extend the network. Network branches are implemented with special splitters. Extremely robust, three-pole XLR (Canon) connectors are used to connect all DMX devices, which is ideally suited for stage use.

The DMX512 standard supports up to 512 device addresses. Depending on how many addresses a component needs, the number of devices that can be operated on a bus varies.

# DMX Lighting

In this article, I use two simple DMX lights that I ordered directly from China [1] some time ago for EUR6.58 each. However, ordering directly from China now might not be worth the effort and prices have increased, so find out in advance what additional costs you will have to pay.

The lamps have eight channels each, which means they occupy eight addresses on the DMX bus. If you assign address 1 to the first lamp, the second lamp is assigned address 9. Somewhat confusingly, addresses and channels are talked about in the DMX environment as if they were different things. The rule of thumb is that you should have an address for each channel in the light.

Table 1 shows an overview of the channels for the hardware I used.

Most of the functions the DMX lamps offer are self-explanatory. Only a few items require special attention. For the spot to illuminate, you need a value greater than 0 on channel 1. You can’t turn up just the red dimmer while the general dimmer is set to 0.

A value of 0 disables the strobe (channel 6). At a value of 1, it flashes at maximum rate and slows with an increase in value. Various predefined color scenarios can be selected in Auto Run operational mode...

![](bbox=[0.9, 0.75, 0.93, 0.9])