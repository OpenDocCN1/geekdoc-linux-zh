```
$ ps axf

3356 ?    Ss   0:00 /bin/dd bs 1 if /proc/kmsg of /var/run/klogd/kmsg
3358 ?    Ss   0:00 /sbin/klogd -P /var/run/klogd/kmsg
3377 ?    Ss   0:00 /usr/bin/ dbus-daemon --system
3392 ?    S    0:02 /usr/sbin/hald
3393 ?    S    0:00 \¬\ hald-runner
3410 ?    S    0:49 \¬\ \¬\ /usr/lib/hal/hal-addon-storage
3666 ?    S    0:00 /usr/sbin/gdm
3674 ?    S    0:03 \¬\ /usr/sbin/gdm
3679 tty7 Ra+ 1548:41 \¬\ \¬\ /usr/bin/X :0 -br -audit 0 -auth /var/lib/g
4850 ?    Ss   0:02 \¬\ x-session-manager
4892 ?    Ss   0:00 \¬\ \¬\ /usr/bin/ssh-agent /usr/bin/dbus-launch -
3737 ?    Ssl  0:00 /usr/sbin/hpiod
3746 ?    S    0:01 python /usr/sbin/hpssd
```

In the Linux world, you can find a number of programs devoted to deciphering those numbers, thereby making it possible to find out what processes are doing and how much time and resources they are using to do it and making it possible to retrieve the resultant information.

# Interrupting, Suspending, and Restarting Processes

Once in a while, I start a process that I think is going to take a few seconds—like parsing a large log file, scanning for some text, extracting something else, sorting the output, and finally sending the whole thing to a file. All of these are very ad hoc in terms of reporting. The trouble is this: Two and a half minutes go by and I start to get a little impatient. Had I thought that the process would take a while, I might have started it in the background.

When you start a process (by typing a command name and pressing <Enter>), you normally start that process in the foreground. In other words, your terminal is still controlling the process and the cursor sits there at the end of the line until the process completes. At that point, it returns to the command or shell prompt. For most (not all) processes, you can run things in the background, thus immediately freeing up your command line for the next task. You do this by adding an ampersand (&) to the end of the command before you press <Enter>.

```
$ sh long_process &
```

However, I've already confessed that I wasn't thinking that far ahead and as a result, I am sitting looking at a flashing cursor wondering if I did some-