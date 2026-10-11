![](bbox=[0.41, 0.1, 0.61, 0.38])

*Figure 11: From the wire to Wireshark*

The secret to using any network sniffer, including Wireshark, is learning how to use capture and display filters to strip out superfluous data. Fortunately, Wireshark’s graphical interface makes it relatively easy to visualize data and work with the various filters.

# 4.4.2 Launching Wireshark

In the following example, we will capture network traffic during an anonymous FTP login. On our Kali system, we launch Wireshark using the command line as shown in Listing 125 or via the application menu, where it is located under the Sniffing & Spoofing sub-menu.

```
kali@kali:~$ sudo wireshark
*Listing 125 - Running wireshark from the terminal*
```

# 4.4.3 Capture Filters

When Wireshark loads, we are presented with a basic window where we can select the network interface we want to monitor as well as set display and capture filters. As mentioned above, we can use capture filters to reduce the amount of captured traffic by discarding any traffic that does not match our filter and narrow our focus to the packets we wish to analyze. Be aware that any traffic excluded from a capture filter will be lost, so it is best to define broad capture filters if you are concerned about potentially losing data.

We’ll start by selecting the interface we would like to monitor and entering a capture filter. In this case, we use the net filter${ }^{105}$ to only capture traffic on the 10.11.1.0/24 address range:

${ }^{105}$ (Berkeley Packet Filter), http://biot.com/capstats/bpf.html