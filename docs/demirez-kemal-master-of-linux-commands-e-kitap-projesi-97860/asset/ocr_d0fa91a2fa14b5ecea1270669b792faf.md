# # Who-Whoami

To find out who is active in the system, who's been login, to find an identity information, we can use w, who, whoami commands.

```
root@kemal:-# w
01:55:59 up 8:17, 2 users, load average: 0.78, 1.06,
USER     TTY             FROM LOGIN@ IDLE JCPU
root     :0               0               17:39 ?xdm? 55:50
root     pts/0           :0               17:48 0.00s 0.58
root@kemal:-#
```

There are uses of these commands. Briefly:

+   - w: To find out the information which user runs at that moment which applications / command.
- who: Identity which profile is worked in the system.
- whoami: Identify whih profile user is working with.

```
root@kemal:-# who              2015-08-22 17:39 (:0)
root     :0
root     pts/0         2015-08-22 17:48 (:0)
root@kemal:-# whoami
root
root@kemal:-# am i
root     pts/0         2015-08-22 17:48 (:0)
root@kemal:-# _
```

When we use who command with -b we can see when the system run last time, with -r shows the opening levels (runlevel).