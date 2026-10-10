ISP with a network on which to place untranslated "edge" machines such as Web servers, mail gateways, and other hosts that need to be accessible from the general Internet.  
A DMZ may or may not be configured to be protected by the firewall rules in the gateway router. Usually this is desirable, but some specialized cases require that the DMZ be exempt from the LAN's firewall rules. Your network situation will dictate your needs.

# ### Enabling the Firewall

IPFW is not supported in the `GENERIC` kernel. As you learned in Chapter 16, you can compile certain options into a custom kernel to enable IPFW, including `IPFIREWALL`, `IPFIREWALL_VERBOSE`, and `IPFIREWALL_VERBOSE_LIMIT=10`. You don't need to build a new kernel, however, in order to use IPFW; it's available as a kernel module, which is loaded automatically by the `/etc/rc.network` script. To enable the firewall without rebuilding the kernel, add the following lines to `/etc/rc.conf`:

```
firewall_enable="YES"  
firewall_type="open"
```

If you don't specify that the firewall type should be `open`, the only rule that IPFW will start with is the default one, with an index of `65535` (the maximum), specifying `deny ip from any to any`. In other words, if you reboot with IPFW in its default configuration, your machine will be completely blocked off from the network, and you'll have to have physical console access to it in order to get it back.

> **CAUTION**  
> It's dangerous to experiment with IPFW if you don't have console access, because it's very easy to put your machine into an unreachable state. Until you are comfortable enough with IPFW to know exactly what you're doing, always make sure you can access the machine via the console in case something goes wrong.
> 
> If you do end up blocking your machine from the network through experimentation with IPFW, the only way to recover is to go to where the machine is physically located and log in from the console. From there, you can disable IPFW by removing the lines in `/etc/rc.conf`, or you can configure it properly and reboot.

The `open` setting changes the default rules so that IP traffic is passed (allowed) by default, rather than blocked. Blocking traffic by default creates a truly secure system, but it can be excessively restrictive for systems that exist within a secure environment. At the same time, allowing traffic by default (blocking only specified IP traffic) eliminates the possibility of having complete system security. Use the `open` setting if your system is in a network that's already behind a firewall; you probably don't need to apply the same kind of protection twice.