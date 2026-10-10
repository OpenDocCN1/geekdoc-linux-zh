```
Active UNIX domain sockets (w/o servers)
Proto RecvCnt Flags    Type State I-Node Path
unix 2 [ ] DGRAM 10825
@org/freedesktop/systemd1/notify
unix 2 [ ] DGRAM 10933
/run/systemd/shutdown
unix 6 [ ] DGRAM 6609
/run/systemd/journal/socket
unix 25 [ ] DGRAM 6611 /dev/log
unix 3 [ ] STREAM CONNECTED 25693
unix 3 [ ] STREAM CONNECTED 20770
/var/run/dbus/system_bus_socket
unix 3 [ ] STREAM CONNECTED 19556
unix 3 [ ] STREAM CONNECTED 19511
unix 2 [ ] DGRAM 24125
unix 3 [ ] STREAM CONNECTED 19535
unix 3 [ ] STREAM 18067
/var/run/dbus/system_bus_socket
unix 3 [ ] STREAM CONNECTED 32358
unix 3 [ ] STREAM 24818
/var/run/dbus/system_bus_socket
...
```

The netstat command produces lots of output because there are normally lots of programs that use network services on Linux systems. You can limit the output to just TCP or UDP connections by using the -t command-line option for TCP connections or -u for UDP connections:

```
$ netstat -t

Active Internet connections (w/o servers)
Proto Recv-Q Send-Q Local Address Foreign Address State
tcp 1 0 10.0.2.15:58630 productsearch.ubu:https CLOSE_WAIT
tcp6 1 0 [::]localhost:57782 [::]localhost:ipp CLOSE_WAIT
$
```

You can also get a list of what applications are listening on which network ports by using the -l option:

```
$ netstat -l
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address Foreign Address State
tcp 0 0 ubuntu02:domain *.* LISTEN
tcp 0 0 localhost:ipp *.* LISTEN
tcp6 0 0 [::]localhost: [::]:* LISTEN
```