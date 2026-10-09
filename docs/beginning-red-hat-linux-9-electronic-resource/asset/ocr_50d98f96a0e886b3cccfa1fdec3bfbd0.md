# Red Hat Linux 9 Basics

![](bbox=[0.18, 0.08, 0.84, 0.31])

We can see from the figure above that the only Ethernet controller in this list is a Realtek 8139/8139C/8139C+ model. Note that this output also confirms the other devices on the system – like the audio card, the TV tuner, and the video card of the system. We'll make use of this when we cover these devices later in the chapter.

We can confirm whether this Ethernet controller is the one configured as the `eth0` device by checking the network driver loaded for this device. To do this, take a look at the contents of the file `/etc/modules.conf`. This file specifies the drivers to be loaded for various devices and their corresponding loading parameters:

![](bbox=[0.18, 0.52, 0.84, 0.71])

In the second line of the file in the figure above we find an instruction for loading the `8139too` driver for the `eth0` device. This confirms that the `eth0` network device is actually a Realtek network card. Incidentally, the third line of this file reveals that the audio card on the machine is a VIA82xxx family audio controller.

Details of the network can be found out by using the `netstat` and the `route` programs. The `route` program displays the network routes active in the system including the gateway through which this desktop sends and receives network traffic from the Internet. The `netstat` program shows the currently active network connections and networking services that are available on the machine. We'll take a look at `netstat` in Chapter 12, and you can learn more about `route` by typing `man route` at the terminal.