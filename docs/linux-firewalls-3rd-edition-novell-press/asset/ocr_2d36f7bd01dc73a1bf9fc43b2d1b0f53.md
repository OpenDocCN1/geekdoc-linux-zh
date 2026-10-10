# Final Thoughts on Snort

Snort comes highly recommended as a means to automate the task of intrusion detection. I’ve only been able to touch on the very basics of Snort here in hopes of giving you a starting point for working with it. From here, you can combine Snort with MySQL and ACID to create an enterprise-class intrusion detection system. Snort can be configured just as you need and extended to fit any size of organization.

# Monitoring with ARPWatch

ARPWatch is a daemon that watches for new Ethernet interfaces on a network. If a new ARP entry is seen, it could be indicative of a rogue computer somewhere within the network.

ARPWatch uses the PCap library, which may not (yet) be on your system. If it’s not, you’ll find out during the configuration process for ARPWatch. The PCap library, commonly known as libpcap, can be downloaded from http://www.tcpdump.org/. The PCap library is used for other network and security-related programs such as TCPDump. Because TCPDump was already covered, I’ll forgo repeating the instructions for installing libpcap in this chapter and instead I’ll refer you to the section “TCPDump: A Simple Overview” for those instructions.

Installation of ARPWatch involves unwrapping the ARPWatch archive that you download, usually something like tar -zxvf arpwatch.tar.Z. From there, change directory into the ARPWatch directory and run the configure script.

```
./configure
```

You’ll see a (hopefully somewhat) familiar series of output statements, something like this:

```
creating cache ./config.cache
checking host system type... i686-pc-linux-gnu
checking target system type... i686-pc-linux-gnu
checking build system type... i686-pc-linux-gnu
checking for gcc... gcc
checking whether the C compiler (gcc ) works... yes
... (output truncated) ...
```

If you see an error to the effect of the following, you’ll need to install libpcap:

```
checking for main in -lpcap... no
configure: error: see the INSTALL doc for more info
```

Refer to the section on TCPDump earlier in this chapter for information on installing the PCap library.