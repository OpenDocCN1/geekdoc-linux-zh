Make sure you check to see whether the line already exists before adding this line because having two GATEWAY lines could cause a conflict.

You will need to restart the Slackware Linux system before the changes take effect.

If you don't want to restart the system, you can add the default route manually with the following command issued from a root shell:

```
route add default gw 64.41.131.162
```

# # Configuring Wireless Internet Access

Wireless network access has recently become very popular because it does not require wires to be strung around, and it also does not require network connection jacks, which eliminates the common problem of not having enough network connection jacks. Any PC that has a wireless networking card can communicate with the network. Indeed, many notebook computers are shipping with wireless networking capabilities built in to them.

One of the most common applications of this technology is Internet sharing for school classrooms. Each student can have a notebook computer on his or her desk and have access to the Internet through a central server.

Configuring FreeBSD to work as a wireless gateway for this type of setup is almost identical to configuring a normal gateway, as already discussed. The only real difference is that you will need to have a wireless networking card installed in the FreeBSD system.

Table 27.1 lists some of the wireless network interfaces that FreeBSD currently supports, along with the corresponding devices that need to be present in the kernel configuration file. Note that support for new devices is being added on a regular basis, so check the hardware compatibility list on the FreeBSD Web site for the latest information.

**TABLE 27.1 Wireless Network Interfaces That FreeBSD Currently Supports**

| Wireless Interface | Kernel Device |
| :--- | :--- |
| Aironet 4500/4800 802.11 | device an |
| AMD Am79C930-based cards | device awi |
| Xircom CNU/NetWare Airsurfer | device cnw |
| Lucent WaveLan 802.11 | device wi |
| Lucent WaveLan (ISA only) | device wl |


With the exception of the cnw and wl devices, support for these adapters is included in the default GENERIC kernel. So, unless you have a wireless network card that requires the cnw device or the wl device, you should be okay unless you built a custom kernel and removed support for these devices.

If you do need to build a new kernel to support your wireless network card, see Chapter 16 for details on how to do this.