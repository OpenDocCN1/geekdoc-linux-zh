This setup is fairly simple, because there are currently no other boxes on my internal network.

I don't want any local process (i.e., Netscape, Lynx, etc.) to connect to doubleclick.net:

```
```
# ipchains -A output -d 199.95.207.0/24 -j REJECT
# ipchains -A output -d 199.95.208.0/24 -j REJECT
# ```
```

Now I want to set priorities on various outgoing packets (there isn't much point in doing it on incoming packets). Since I have a fair number of these rules, it makes sense to put them all in a single chain, called ppp-out.

```
```
# ipchains -M ppp-out
# ipchains -A output -i ppp0 -j ppp-out
# ```
```

Minimum delay for Web traffic & telnet.

```
```
# ipchains -A ppp-out -p TCP -d proxy.virtual.net.au 8080 \
    -t 0x01 0x10
# ```
```

```
```
# ipchains -A ppp-out -p TCP -d 0.0.0.0 telnet -t 0x01 0x10
# ```
```

Low cosr for ftp data, nntp, pop-3:

```
```
# ipchains -A ppp-out -p TCP -d 0.0.0.0/0 ftp-data \
    -t 0x01 0x02
# ipchains -A ppp-out -p TCP -d 0.0.0.0/0 nntp -t 0x01 0x02
# ipchains -A ppp-out -p TCP -d 0.0.0.0/0 pop-3 -t 0x01 0x02
# ```
```

There are a few restrictions on packets coming in the ppp0 interface. Let's create a chain called ppp-in:

```
```
# ipchains -N ppp-in
# ipchains -A input -i ppp0 -j ppp-in
# ```
```

Now, no packets coming in ppp0 should be claiming a source address of 192.168.1.*, so we log and deny them:

```
```
# ipchains -A ppp-in -s 192.168.1.0/24 -l -j DENY
# ```
```

I allow UDP packets in for DNS (I run a caching nameserver that forwards all requests to 203.29.16.1, so I expect DNS replies from them only), incoming ftp, and return ftp data only (which should be going to a port above 1023 and not the X11 ports around 6000).

```
```
# ipchains -A ppp-in -p UDP -s 203.29.16.1 \
    -d $LOCALIP dns -j ACCEPT
```
```