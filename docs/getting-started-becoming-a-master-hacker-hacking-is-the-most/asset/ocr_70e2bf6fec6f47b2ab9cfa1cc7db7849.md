(Berkley Software Development) Unix--utilizes the Berkley Packet Filter (BPF) format to create filters.

We can create that filter for the Windows 7 IP address by entering: kali > tcpdump host 192.168.0.114

Now you can see just the traffic coming and going to the Windows 7 system as we have filtered out all the other traffic.

Now, let's connect to the Apache webserver on our Kali machine from your Windows 7 system. First, start the Apache2 webserver built into Kali.

kali > systemctl apache2 start This starts your Apache webserver. Next, start tcpdump again on your Kali system.



```
root@kali-2019:~# tcpdump host 192.168.0.114
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), capture size 262144 bytes
09:51:51.186494 ARP, Request who-has gateway tell 192.168.0.114, length 46
09:51:51.195764 ARP, Reply_gateway is-at b0:be:76:08:b5:3c (oui Unknown), length 46
09:51:58.212805 ARP, Request who-has 192.168.0.114 tell gateway, length 46
09:51:58.214731 ARP, Request who-has kali-2019 tell 192.168.0.114, length 46
09:51:58.214749 ARP, Reply kali-2019 is-at 08-00-27:9e:13:2d (oui Unknown), length 28
09:51:58.214997 IP 192.168.0.114.49744 > kali-2019.http: Flags [S.], seq 1495846102, win 8192, options [mss 1460, nop, wscale 8, nop, nop, sackOK], length 0
09:51:58.215616 IP kali-2019.http > 192.168.0.114.49744: Flags [S.], seq 1383202157, ack 1495846103, win 29280, options [mss 1460, nop, nop, sackOK, nop, wscale 7], length 0
09:51:58.215228 IP 192.168.0.114.49744 > kali-2019.http: Flags [.], ack 1, win 256, length 0
09:51:58.215496 IP kali-2019.http > 192.168.0.114.49744: Flags [P.], seq 1:441, ack 1, win 256, length 440: HTTP: GET / HTTP/1.1
09:51:58.215429 IP kali-2019.http > 192.168.0.114.49744: Flags [.], ack 237, length 0
09:51:58.216329 IP kali-2019.http > 192.168.0.114.49744: Flags [P.], seq 1:3381, ack 441, win 237, length 3380: HTTP: GET /icons/openlogo-75.png HTTP/1.1
```

```
root@kali-2019:~# tcpdump src host 192.168.0.114
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), capture size 262144 bytes
16:49:36.953749 IP 192.168.0.114.49895 > kali-2019.http: Flags [S.], seq 1049926987, win 8192, options [mss 1460, nop, wscale 8, nop, nop, sackOK], length 0
16:49:36.953924 IP 192.168.0.114.49895 > kali-2019.http: Flags [.], ack 1212929604, win 256, length 0
16:49:36.954000 IP 192.168.0.114.49895 > kali-2019.http: Flags [P.], seq 0:440, ack 1, win 256, length 440: HTTP: GET / HTTP/1.1
16:49:36.955526 IP 192.168.0.114.49895 > kali-2019.http: Flags [.], ack 3381, win 256, length 0
16:49:36.957218 IP 192.168.0.114.49895 > kali-2019.http: Flags [P.], seq 440:849, ack 3381, win 256, length 409: HTTP: GET /icons/openlogo-75.png HTTP/1.1
```

kali > tcpdump host 192.168.0.114