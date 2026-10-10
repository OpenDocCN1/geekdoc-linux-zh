To use the modules, simply make sure to insmod them at boot time. For example, if you want to support Real Audio and FTP masquerading, add the following to your boot script:

```
```
insmod ip_masq_ftp
insmod ip_masq_audio
```
```

> NOTE: Most distributions come with these kernel modules precompiled. If you choose to compile your own kernel, be sure to select these features while configuring the kernel, or you'll have nothing to insmod!

# ## SUMMARY

In this chapter we discussed the tools needed to perform advanced network administration under Linux. Specifically, we covered the techniques for using IP aliasing, packet filters, and IP masquerading. Given what we have discussed, it is possible for you to set up a simple Linux router with multiple IP addresses and perform basic firewalling and NAT functions for a network.

The key tool for all of this is ipchains. With it, you can manipulate a significant amount of detail in how Linux processes packets entering, leaving, or passing through it. With the ability to add arbitrary chains to the mix, with one chain being able to point to another chain and so forth, the potential complexity is truly amazing.

If you are interested in learning more about Linux networking, there are plenty of Web sites you can learn from. At the top of the list is http://sana.freedom.org/linux/2.2, which contains a wonderful summary of tools, documentation, and links to more information about Linux networking. For more about IP Masquerading, visit http://jmanzink.kernelsource.org and http://ipmasq.cjb.net, where you can find up-to-the-minute news, developers, and of course, documentation on tools and techniques. Finally, there is the official home page for the ipchains tool, http://www.rustcorp.com/linux/ipchains.

If you’re feeling adventurous, you can learn about the next generation of ipchains called ‘netfilter’ at http://netfilter.kernelsource.org. This requires that you run the kernel version 2.3 or later. Its documentation is still sketchy, but for some of us that’s half the fun.

If you’re impressed with Linux networking (and you should be!), but you don’t have time to administer a Linux-based router/firewall yourself, take a look at the Firebox at http://www.watchguard.com.