listed by ls and are called hidden filenames [page 192].) You may find it helpful to create a .plan file for yourself; it can contain any information you choose, such as your schedule, interests, phone number, or address. In a similar manner, finger displays the contents of the .project and .pgpkey files in your home directory. If Alex had not been logged in, finger would have reported only his user information, the last time he logged in, the last time he read his email, and his plan.

You can also use finger to display a user's username. For example, on a system with a user named Helen Simpson, you might know that Helen's last name is Simpson but might not guess that her username is hls. The finger utility, which is not case sensitive, can search for information on Helen using her first or last name. The following commands find the information you seek as well as information on other users whose names are Helen or Simpson:

```
$ finger HELEN
Login: hls                                Name: Helen Simpson.
...
```

```
$ finger simpson
Login: hls                                Name: Helen Simpson.
...
```

See page 374 for information about using finger over a network.

# W: LISTS USERS ON THE SYSTEM

The w utility displays a list of the users who are logged in. As discussed in the section on who, the information that w displays is useful when you want to communicate with someone at your installation.

The first column in Figure 5-13 shows that Alex, Jenny, and Scott are logged in. The second column shows the designation of the device that each user's terminal is connected to. The third column shows the system that a remote user is logged in from. The fourth column shows the time when each user logged in. The fifth column indicates how long each user has been idle (how much time has elapsed since the user pressed a key on the keyboard). The next two columns identify how much computer processor time each user has used during this login session and on the task that is running. The last column shows the command each user is running.

```
      $ w
      8:20am up 4 days, 2:28, 3 users, load average: 0.04, 0.04, 0.00
      USER   TTY        FROM    LOGIN@  IDLE   JCPU   PCPU  WHAT
      alex   pts/4     :0      5:55am  13:45  0.15s  0.07s  w
      alex   pts/5     :0      5:55am  27      2:55   1:01   bash
      jenny  pts/7     bravo   5:56am  13:44  0.51s  30s    vim 3.txt
      scott  pts/12    bravo   7:17pm        1.00s  0:14s  run_bdgt
```

Figure 5-13 The w utility