# 456 SYSTEM ADMINISTRATION: CORE CONCEPTS

you kill it for Sam. First use ps with the -u option, followed by the name of the user and the -f (full/wide) option to view all processes associated with that user:

```
$ ps -u sam -f
|UID PID PPID C STIME TIME CMD |
|sam 2294 2259 0 09:31 ? 00:00:00 / /bin/sh /usr/bin/startkode |
|sam 2339 2294 0 09:31 ? 00:00:00 /usr/bin/sshd-agent /usr/bin/dbus-launch |
|sam 2342 1 0 09:31 ? 00:00:00 daus-daemon --fork --print-id 8 --prin |
|sam 2433 1 0 09:31 ? 00:00:00 /usr/bin/dbus-launch --exit-with-session |
|sam 2396 1 0 09:31 ? 00:00:00 kdeinit Running... |
|sam 2399 1 0 09:31 ? 00:00:00 gnome-dbus [kdeit] --nosid |
|sam 2401 2396 0 09:31 ? 00:00:00 klaunchlauncher [kdeit] |
|sam 2403 1 0 09:31 ? 00:00:00 kde [kdeit] |
|sam 2405 1 0 09:31 ? 00:00:00 /usr/libexec/game_server |
|sam 2413 2396 0 09:31 ? 00:00:00 /usr/bin/artsd F 10 -S 4096 -s 60 -m a |
|sam 2415 1 0 09:31 ? 00:00:00 kcache [kdeit] |
|sam 2416 2294 0 09:31 ? 00:00:00 kwrapper kmserver |
|sam 2418 1 0 09:31 ? 00:00:00 kmserver [kdeit] |
|sam 2421 2396 0 09:31 ? 00:00:00 kwm [kdeit] -session 1070626ea6a0001 |
|sam 2424 1 0 09:31 ? 00:00:01 desktop [kdeit] |
|sam 2426 1 0 09:31 ? 00:00:01 kicker [kdeit] |
|sam 2429 2396 0 09:31 ? 00:00:00 koi_file /tmp/socket-ma |
|sam 2434 2396 0 09:31 ? 00:00:00 konsole [kdeit] -session 1070626ea6a |
|sam 2435 2396 0 09:31 ? 00:00:00 /bin/sh /usr/lib/firefox/firefox-1.5/run-moz -U |
|sam 2440 1 0 09:31 ? 00:00:00 /bin/sh /usr/lib/firefox-1.5/firefox -UIIoc |
|sam 2453 2434 0 09:31 pts/2 00:00:00 /bin/bash |
|sam 2474 1 0 09:31 ? 00:00:00 /usr/libexec/qconfd-2 10 |
|sam 2482 1 0 09:32 ? 00:00:00 synergetic cm |
|sam 3568 3567 0 13:55 pts/3 00:00:00 -bash |
|sam 3726 1 0 14:07 ? 00:00:00 notify [kdeit] |
|sam 3728 1 0 14:07 ? 00:00:00 /usr/bin/artsd F 10 -S 4096 -s 60 -m a |
|sam 3730 2424 0 14:07 ? 00:00:00 gnome-calculator |
|sam 3731 3568 0 14:07 pts/3 00:00:00 ps -u sam -f |
```

This list is fairly sort, and running gnome-calculator is easy to find. Another way to search for this process is to use ps to produce a list of all processes and then use grep to find which one is running gnome-calculator:

```
$ ps -ef | grep gnome-calculator
|sam 3730 2424 0 14:07 ? 00:00:00 gnome-calculator |
|sam 3766 3568 0 14:14 pts/3 00:00:00 gnome-calculator |
```

If several people are running gnome-calculator, look in the left column to find the correct username so you can kill the process. You can combine the two commands as ps -u sam -f | gnome-calculator:

Now that you know Sam's process running gnome-calculator has a PID of 3730, which you could allow him to log in for. The safest way is to log in as Sam (perhaps you could) and run any of the following commands which send a terminal signal to 3730):

```
kill 3730
```

or