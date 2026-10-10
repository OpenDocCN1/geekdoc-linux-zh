189  -1  klog  pseudo
193  -1  mux2  tty
203  -1  sctl  ctl
205  -1  tape  tape
207  -1  sy  pseudo
216  -1  CentIF  ext_bus
227  -1  kept  pseudo
229  -1  ite  graf_pseudo

And last, here is an example of running **lsdev** on the same V-class server on which the first **ioscan** was run:

```
```
$ /usr/sbin/lsdev

                              (on V-Class)
```
```

Character     Block    Driver      Class
0           -1       cn        pseudo
3           -1       mm        pseudo
16          -1       pty0m     pty0m
17          -1       pty1e     pty1e
27          -1       dmem      pseudo
28          -1       diag0     diag
46          -1       netdiag1  unknown
64          64       lv        lvm
69          -1       dev_config pseudo
72          -1       clone     pseudo
73          -1       strlog    pseudo
74          -1       sad       pseudo
75          -1       telm      strtelm
76          -1       tels      strtels
77          -1       ticlts    pseudo
78          -1       tlcots    pseudo
79          -1       tlcootad  pseudo
114         -1       ip        pseudo
115         -1       arp       pseudo
116         -1       echo      pseudo
119         -1       dlpi      pseudo
130         -1       rawip     pseudo
136         -1       tcp       pseudo
137         -1       udp       pseudo
138         -1       stopmap   pseudo
139         -1       nuls      pseudo
140         -1       netgq     pseudo
141         -1       tun       pseudo
142         -1       fddi4     unknown
143         -1       fc71_ctl  lan
144         -1       fcgsc_lan lan