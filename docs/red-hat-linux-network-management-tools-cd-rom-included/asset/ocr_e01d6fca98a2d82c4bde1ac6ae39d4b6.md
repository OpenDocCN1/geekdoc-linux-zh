Alternatively, you could just display one of the listed protocols instead of the entire list. In this situation, use one of the `--raw`, `--tcp`, or `--udp` keyword options. Then, only that protocol will be displayed. For instance, to display just IP and ICMP packets, use the following command:

```
netstat --statistics --raw
```

As a result of this command, the following would be displayed:

```
Ip:
    3360 total packets received
    0 forwarded
    0 incoming packets discarded
    213 incoming packets delivered
    3090 requests sent out
Icmp:
    489 ICMP messages received
    0 input ICMP message failed.
    ICMP input histogram:
    destination unreachable: 486
    echo replies: 3
    487 ICMP messages sent
    0 ICMP messages failed
    ICMP output histogram:
    destination unreachable: 487
```

# Additional Command-line Options

Some additional options are available with the **netstat** command; these include the `-t` option, which is used to control the display of numeric addresses versus trying to determine symbolic hostname, port, or usernames. Use this option when name-resolution services such as DNS or NIS do not function correctly or are unavailable. The default behavior for **netstat** is to display hostname and other symbolic information. The **netstat** command will display the current TCP connections on the local system:

Proto Recv-O Send-O Local Address Foreign Address State
    tcp 0 126 socrates.home.co:telnet durer.home.com:1035 ESTABLISHED

However, when the `-t` option is added, the following is displayed:

Proto Recv-O Send-O Local Address Foreign Address State
    tcp 0 126 10.0.2.201:23 10.0.2.10:1035 ESTABLISHED