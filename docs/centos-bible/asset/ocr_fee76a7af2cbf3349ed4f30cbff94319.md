and IP address properly listed in the `/etc/hosts` file locally. The former option will probably require that you have one or more DNS servers identified to resolve the name.

If you can reach another computer on the wireless LAN but not computers outside of that LAN (such as Internet addresses), check that you have properly identified the location of your gateway. If the gateway address is correct and you can reach that gateway, it may be that the gateway itself is not configured to allow packet forwarding.

If you find that any of the preceding information needed to be changed and you changed it, you should restart the wireless LAN interface. One way to do that is to restart the PCMCIA interface and the network interfaces as follows:

```
`# /etc/init.d/pcmcia restart`
`# /etc/init.d/network restart`
```

# Adapting to Poor Reception

Your wireless LAN might be working fine while your two wireless computers are sitting on the same desk. But if performance degrades when you separate the computers, you may need to identify any potential obstructions. Then you must decide how to get around them. For desktop systems, a small indoor antenna can bring the signal out from under a desk or out of a closet. For adjacent buildings, a roof antenna might be the answer.

In cities or other congested areas, many people and pieces of equipment can be competing for the 2.4-GHz range. You may want to move a microwave oven or high-end remote phone that may be interfering with your wireless LAN. These settings might help adapt for poor reception:

+   ■ **Reduce Transmission Rate** — Instead of using 11 Mbps, you can explicitly ramp down to 5.5, 2, or 1 Mbps. Slower rates can mean more efficient operation in noisy places.
+   ■ **Use Smaller Fragment Sizes** — Although there is more total overhead to transmitting packets broken up into smaller fragments, they can often provide better overall performance in noisy environments. Change the `frag` parameter to reduce fragment sizes.
+   ■ **Use Different Frequencies** — By specifically requesting that certain frequencies (or channels) be used for transmission, you can avoid congested channels.

# Use Debugging Tools

Because most wireless LAN cards were created for Windows systems, debugging tools from the manufacturers are available only on those systems. If your computer is a dual-boot system (Windows and Linux), try booting in Windows to test the quality of your wireless network.

In CentOS, you can use many of the tools you use for wired Ethernet networks and other TCP/IP network interfaces. Here are a couple of examples.

+   ■ **Wireshark** — The Wireshark window (type `wireshark` as the `root` user from a Terminal window) lets you watch Ethernet frames being sent and received by your wireless LAN interface. For example, the output of Wireshark can tell you whether a failed connection reflects a lack of reception or rejected requests. (Wireshark is described in the next section.)