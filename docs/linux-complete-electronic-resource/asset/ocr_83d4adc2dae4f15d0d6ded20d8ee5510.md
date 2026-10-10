into 30 discrete 64kbps B channels with one 64kbps D channel. Any number of channels may be used at a time and in any combination. You could, for example, establish 30 separate calls to 50 different destinations at 64kbps each, or you could establish 15 calls to 15 different destinations at 128kbps each (two channels used per call), or just a small number of calls and leave the rest idle. A channel may be used for either incoming or outgoing calls. The original intention of ISDN was to allow telecommunications companies to provide a single data service that could deliver either telephone (via digitized voice) or data services to your home or business without requiring you to make any special configuration changes.

There are a few different ways to connect your computer to an ISDN service. One way is to use a device called a “Terminal Adaptor,” which plugs into the Network Terminating Unit that your telecommunications carrier installed when you got your ISDN service and which presents a number of serial interfaces. One of those interfaces is used to enter commands to establish calls and configuration, and the others are actually connected to the network devices that will use the data circuits when they are established. Linux will work on this sort of configuration without modification; you just treat the port on the Terminal Adaptor like you would treat any other serial device. Another way, which is what the kernel ISDN support is designed for, allows you to install an ISDN card into your Linux machine and then has your Linux software handle the protocols and make the calls itself.

# Kernel Compile Options:

```
ISDN subsystem -->
<> ISDN support
[] Support synchronous PPP
[] Support audio via ISDN
< ICN 2B and 4B support
<> PCBIT-D support
<> Teles/NIccy1016PC/Creatix support
```

The Linux implementation of ISDN supports a number of different types of internal ISDN cards. These are those listed in the kernel configuration options:

+   * ICN 2B and 4B
+   * Octal PCBIT-D
+   * Teles ISDN-cards and compatibles