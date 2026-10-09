```
www.google.com has address 173.194.46.80

www.google.com has IPv6 address
2607:f8b0:4009:805::1013

$ ping -cl !

ping -cl www.google.com

PING www.google.com (173.194.46.80) 56(84) bytes of data.
64 bytes from ord08s11-in-f16.l.google.net
(173.194.46.80): icmp_seq=1 ttl=51 time=17.0 ms
--- www.google.com ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 49ms

rtt min/avg/max/mdev = 17.071/17.071/17.071/0.000 ms
$ 
```

# # Reuse the Last Word (Last Argument) from the Previous Command

```
$ !$
```

Quite often I find myself needing to perform another operation on the last item on the previous command line. To access that item in your current command, use '!$'.

```
$ unzip tpstreport.zip
Archive: tpstreport.zip
inflating: cover-sheet.doc
$ rm !$
rm tpstreport.zip
$ mv cover-sheet.doc reports/
$ du -sh !$
```