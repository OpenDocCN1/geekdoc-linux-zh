Finally, build and install tcpdump.

```
cd ../tcpdump-3.4
./configure
make
su
make install
make install-man
```

If you are using csh, issue the rehash command. To watch ARP packets, the following is a starting point:

tcpdump arp

Similarly, ICMP packets can be watched

```
tcpdump icmp
```

# 8.13.2 Using tcpdump

Some of tcpdump's more useful flags are discussed here. The -i flag is used to specify which interface to use. The -l flag causes tcpdump to line-buffer the output if it is not going to a tty. This is useful in the following, where immediate output to the screen is desired, as well as capture in a file for later detailed analysis.

```
tcpdump -l other options | tee foo
```

or

```
tcpdump -l other options > foo& tail -f foo
```

The -N flag chops displayed host names at the first. Following any flags is an optional expression that specifies which packets should be dumped. The absence of an expression will cause all packets to be dumped. If you run tcpdump over a networked net or X session, this I/O will be displayed. (Think "infinite loop.") An expression is similar to that in a language or the find program.

Some of the "primitive" elements that may be used to build expressions include the following:

+   - type
This is something of a misnomer, selecting by host, net, or port. Each of these takes a speculator, for example, host name or IP address. The net primitive will accept address/bits, where address is an IP address and bits is the number of order bits to match. Thus, to match Pentacorp's class-B network, use

```
tcpdump 192.168.0.0/16
```