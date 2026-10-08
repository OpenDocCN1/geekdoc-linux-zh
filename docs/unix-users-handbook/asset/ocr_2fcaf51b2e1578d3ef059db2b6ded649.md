Processing section "[home]"
Processing section "[/home/martyp]"
Loaded services file OK.
WARNING: You have some share names that are longer than 8 chars
These may give errors while browsing or may not be accessible to some older clients
Press enter to see a dump of your service definitions
•
•
•

**testparm** produced the warning for a long share name and also included a list of our three shares, which looked to be in order. We won't address the long share name warning because the Windows system used in the example can handle the long name. If, however, we were on a DOS system, there would be a problem with this name. We'll see shortly how these potential name icoompatibilities are addressed by Linux.

The next check we want to perform is to see that the daemon for Samba called **smbd** is indeed running, as shown in the following listing:

![](bbox=[0.03, 0.56, 0.12, 0.65])

```
# ps -efl | grep smbd

140  S  root   490   1  0  60   0 -   553 do_sel Sep28 ? 00:00:00 [smbd]
140  S  root  1493  490  0  60  0 -   896 do_sel Sep29 ? 00:00:00 smbd -D
000  S  root  1976 1951  0  70  0 -   288 pipe_r 09:09 pts/1 00:00:00 grep smbd
```

This **ps** output shows that **smbd** is running. Next let's check that the **netbios-ssn** service is running in the "LISTEN" state, as shown in the following example:

![](bbox=[0.03, 0.7, 0.12, 0.8])

![](bbox=[0.03, 0.81, 0.12, 0.9])

```
# netstat -a | grep netbios

tcp   0  0 linux1:netbios-ssn   f4457mf2:1047        ESTABLISHED
tcp   0  0 :netbios-ssn   *:                 LISTEN
udp   0  0 linux1:netbios-dgm   *:*
udp   0  0 linux1:netbios-ns   *:*
udp   0  0 :netbios-dgm   *:*
udp   0  0 :netbios-ns   *:*
```