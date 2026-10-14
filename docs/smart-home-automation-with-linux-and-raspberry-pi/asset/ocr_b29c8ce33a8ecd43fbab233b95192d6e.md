pair, a remote trigger, or a scene trigger (the latter being the C-Bus term for macro programming, where several state changes can occur on several devices at the same time). Scene programming can also occur through the C-Bus Toolkit Software, although this is currently available only for Microsoft Windows.

There are several devices in each family, capable of various support loads and characteristics, but generally speaking a C-Bus dimmer will support incandescent and halogen lamps between 25W to 500W (up to 2A), along with fan motors (up to 2A).

These two series also provide basic switch units. These appear the same as their lamp-controlling counterparts, except that they lack the dim functionality. By way of compensation, they can support a much greater range of devices (up to 2KW, and 8A in places) including fluorescent lights.

> **Note**  There appear to be no in-wall units for sale, meaning you cannot use wireless C-Bus electronics with your own style of face plate.

# Controlling Appliances

Like X10, C-Bus provides an appliance module that plugs into the wall and controls the flow of current to its corresponding socket. These are known as the 5812 series plug-in adapters and look like their X10 counterparts, with the exception that they, too, support dimming and switch versions.

Because every C-Bus device includes a microcontroller and the C-Bus protocol supports the remote programming of other devices, any of the light switches mentioned earlier can also be used to control an appliance switch by programming an “association” on the switch, equivalent to a Linux symbolic link.

# Controllers

The Series Wireless remote control 5888 is the main device here. It is an RF transmitter (operating at 433.92 MHz) supporting ten devices up to 70 meters away (although 25 is more likely inside a building). Because of the unified design of all C-Bus modules, it is technically possible to control more than the allotted ten devices by using the remote to control one switch, which in turn controls another two through the use of a scene. Furthermore, no RF gateway is required to use this remote, since the C-Bus wireless network is already operating on RF. This also means that multiple remotes can control any individual device, and any individual button can control multiple devices.

Like X10, it also supports an “all off” message.

# Gateways

With so much emphasis on the wireless network, it is sometimes necessary to revert to wires. This is where the Wireless Gateway C-Bus 5800 Series comes in. This is a necessary feature and the only way that the wired and wireless versions of C-Bus can be connected together. Also, through the use of software such as C-Bus Toolkit, it can be connected to a computer for remote, sequenced, and intelligent control. Consequently, this device is also necessary for a wireless-only network that needs to feature PC control because the 802.11 wireless protocol used by commercial routers is not suitable as a C-Bus wireless gateway.

# Lighting Control

In addition to the general purpose appliance controls that I’ve discussed, there are also a number of specific controllers for lighting. This is a recent development, but not a great surprise, since lighting is one of the major contributing factors in uptake for home automation. Most of us start with a controller light switch, after all. Given that lights are a specific case, it is therefore possible to add extra functionality to the communication protocols which would make no sense if it were a traditional appliance, such as colour.