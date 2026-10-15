```
[jdoe@frazzi init.d]$ w; who
5:05am up 42 days, 18:42, 22 users, load average: 0.44, 0.40, 0.38
USER     TTY      FROM         LOGIN@   IDLE   JCPU   PCPU   WHAT
root     vc/1     -            15Dec02  42days  0.06s  0.06s  -bash
ejray    pts/0     -            16Dec02  41days  0.00s  ?      -
ejray    pts/1     -            Sat 6am  12:28m 0.88s  0.77s  ssh mike
ejray    pts/2     -            28Dec02  28days  0.25s  0.25s  /bin/zsh
jdoe     pts/6     192.168.1.104 4:58am 1:12 0.02s  0.02s  tail -f /var/log/httpd/
ejray    pts/19    mike.raycomm.c Sat12pm 12:28m 1.05s  0.94s  ssh sulley
root     vc/1
 :0      Dec 15 10:25
         Dec 16 16:10
ejray    pts/0
         Dec 16 16:11
ejdoe    pts/6
         Jan 27 04:58 (192.168.1.104)
ejray    pts/8
         Dec 23 19:49
ejray    pts/17
         Jan 7 18:29
ejray    pts/20
         Jan 4 08:31
jdoe     pts/16
         Jan 13 19:39 (192.168.1.104)
ejray    pts/19
         Jan 25 12:03 (mike.raycomm.com)
ejray    pts/22
         Jan 25 12:03
[jdoe@frazzi init.d]$ last
jdoe     pts/6     192.168.1.104 Mon Jan 27 04:58 still logged in
jdoe     pts/6     192.168.1.104 Mon Jan 27 04:57 - 04:58 (00:01)
jdoe     pts/6     192.168.1.104 Mon Jan 27 04:55 - 04:57 (00:01)
jdoe     pts/6     192.168.1.104 Sun Jan 26 18:05 - 20:16 (02:11)
jdoe     pts/6     mike.raycomm.c Sat Jan 25 12:12 - 06:52 (18:40)
ejray    pts/19    mike.raycomm.c Sat Jan 25 12:03 still logged in
ejray    pts/19    mike.raycomm.c Sat Jan 25 12:02 - 12:02 (00:00)
jdoe     pts/6     mike.raycomm.c Sat Jan 25 10:35 - 12:11 (01:36)
jdoe     pts/19    192.168.1.104 Tue Jan 21 20:59 - 00:11 (03:12)
jdoe     pts/19    192.168.1.104 Mon Jan 13 20:59 - 23:56 (02:57)
jdoe     pts/16    192.168.1.104 Mon Jan 13 19:39 - 23:34 (03:54)
jdoe     pts/23    192.168.1.104 Sun Jan 12 06:02 - 08:14 (02:12)
jdoe     pts/14    192.168.1.104 Mon Jan 6 20:54 - 23:42 (02:47)
ejray    pts/17    frazzi.raycomm.co Thu Jan 2 20:50 - 06:27 (1:09:36)
ejray    pts/4     Wed Jan 1 04:55 gone - no logout
wtmp begins Wed Jan 1 04:55:40 2003
[jdoe@frazzi init.d]$
```

Code Listing 16.5 You can keep an eye on the users logged in and where they're coming from using w; who and last.