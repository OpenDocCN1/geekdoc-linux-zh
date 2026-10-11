This does not display real-time output to the screen but captures the packets on the network to the file named capturefile.cap. Take great care not to leave this capture process running for extended periods of time because filling up your system's root partition can crash the machine or make it unavailable.

To view the data contained in the capture file, such as FTP packets, you would use the following command:

```
tcpdump -r capturefile.cap dst port 21
```

This shows output similar in format to

```
01:42:27.452770 192.168.1.101.2659 > 192.168.1.2.ftp:
➡S 2841408587:2841408587(0) win 64240 <mss1460,nop,nop,sackOK> (DF)
01:42:27.452935 192.168.1.101.2659 > 192.168.1.2.ftp:
➡S. ack 2413194434 win 64240 (DF)
01:42:27.567524 192.168.1.101.2659 > 192.168.1.2.ftp:
➡. ack 50 win 64191 (DF)
01:42:31.216098 192.168.1.101.2659 > 192.168.1.2.ftp:
➡P 0:13(13) ack 50 win 64191 (DF)
```

![](bbox=[0.11, 0.48, 0.23, 0.58])

> Although tcpdump shows up on the exam objectives, I've never seen a question more complex than asking which utility you might use to see the contents of packets, nor have my attendees, of which there have been hundreds. So, don't spend too much time worrying over tcpdump for the exam.

![](bbox=[0.11, 0.58, 0.23, 0.68])

> To get a refresher on how PPP works, see Chapter 4, "Linux and Hardware," which discusses PPP. The exams both have PPP items on them, but that section covers the objectives and more.