from the `ifconfig` command (described in more detail in Chapter 8, “Configuring Basic Networking”):

```
$ ifconfig eth0
eth0      Link encap:Ethernet  HWaddr 00:0C:76:96:A3:73
          inet addr:192.168.1.3  Bcast:192.168.1.255  Mask:255.255.255.0
          inet6 addr: fe80::20c:76ff:fe96:a373/64 Scope:Link
          UP BROADCAST NOTRAILERS RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:71273424  errors:0  dropped:0  overruns:0  frame:0
          TX packets:5273519  errors:0  dropped:0  overruns:0  carrier:0
          collisions:0  txqueuelen:1000
          RX bytes:6272843708 (5982.2 Mb)  TX bytes:1082453585 (1032.3 Mb)
          Interrupt:10 Base address:0xde00
```

Unfortunately, most of this information is extraneous for the desired purpose. The hardware address is the 6-byte hexadecimal number following `HWaddr`. To extract that data, you can combine `grep` (described shortly, in “Using `grep`”) with `cut` in a pipe:

```
$ ifconfig eth0 | grep `HWaddr` | cut -d " " -f 11
00:0C:76:96:A3:73
```

Of course, in a script you would probably assign this value to a variable or otherwise process it through additional pipes. Chapter 9 describes scripts in more detail.

# Obtaining a Word Count with `wc`

The `wc` command produces a word count (that’s where it gets its name), as well as line and byte counts, for a file:

```
$ wc file.txt
308 2343 15534 file.txt
```

This file contains `308` lines (or, more precisely, `308` newline characters), `2,343` words; and `15,534` bytes. You can limit the output to the newline count, the word count, the byte count, or a character count with the `--lines` (`-l`), `--words` (`-w`), `--bytes` (`-c`), or `--chars` (`-m`) option, respectively. You can also learn the maximum line length with the `--max-line-length` (`-L`) option.

![](bbox=[0.13, 0.79, 0.2, 0.86])

> For an ordinary ASCII file, the character and byte counts will be identical. These values may diverge for files that use multi-byte character encodings.