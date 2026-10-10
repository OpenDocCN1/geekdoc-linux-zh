The only other thing you should need to do is configure your Windows, Macintosh, or other client to use the new gateway server. This will be covered later on in this chapter in the “Configuring Clients to Use the New Gateway” section.

# Using Kernel PPP or a Dedicated Ethernet Connection to the Internet

If you are using Kernel PPP or you have a dedicated Internet connection (ADSL, cable, T1, OC3, and so on), the configuration is a little more complicated. In this case, you will need to use the NAT daemon (natd), which requires a firewall in order to work. To enable the firewall, you will need to build a new kernel. This is not difficult to do, however. You can simply add the following two lines to your kernel configuration file:

```
```
options IPFIREWALL
options IPDIVERT
```
```

You can add to the kernel configuration file various other options that have to do with the firewall, such as logging. A detailed discussion of firewalls is beyond the scope of this chapter, but you may want to read the “Configuring a Firewall” section of Chapter 29, “Network Security,” before you build a new kernel with firewall support. This way, you won’t have to build yet another kernel if you later decide you want another option for the firewall that you didn’t include in the kernel the first time around.

Also, if you are unclear about how to build a new kernel, see Chapter 16, “Kernel Configuration,” for more details.

Once you have finished building a new kernel, you will need to enable natd.

# Configuring and Enabling natd

The NAT daemon natd can be enabled either by configuring network settings in Sysinstall or by manually editing the /etc/rc.conf file. Once again, if you already have basic networking set up, it is easier to simply make the necessary changes manually rather than go through Sysinstall, so this is the method we are going to cover here.

Open the file /etc/rc.conf in your favorite text editor and add the following lines:

```
```
natd_enable="YES"
natd_interface="ppp0"
```
```

The natd_interface line in the previous example assumes that you have a modem connection to the Internet and that it is on the interface ppp0. If you have a dedicated connection over an Ethernet device (such as ADSL, cable, T1, or OC3), you should replace ppp0 with whatever network interface your connection to the outside world runs on.

A few other options to natd are available that control things such as logging. If you are interested in the other options, see the man page for natd.