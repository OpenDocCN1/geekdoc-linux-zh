
Use `whoami` to output the username of the user that is logged in at your terminal. This is not as inutile a command as one might first think—if you’re at a shared terminal, it’s useful to determine whether or not it is your account that you’re messing in, and for those with multiple accounts on a system, it’s useful to see which of them you’re currently logged in with.

To output your username, type:

```
$ whoami [RET]
will
$
```

In this example, the username of the user logged in at this terminal is "will."

## 2.6.2 Listing Who Is on the System

Use `who` to output a list of all the users currently logged in to the system. It outputs a minimum of three columns, listing the username, terminal location, and time of login for all users on the system. A fourth column is displayed if a user is using the X Window System; it lists the window location of the user’s session (see Chapter 4 [The X Window System], page 95).

To see who is currently logged in, type:

```
$ who [RET]
murky    tty1     Oct 20 20:09
dave     tty2     Oct 21 14:37
kurt     tty3     Oct 21 15:04
kurt     ttyp1    Oct 21 15:04 (:0.0)
$
```

The output in this example shows that the user murky is logged in on tty1 (the first virtual console on the system), and has been since 20:09 on 20 October. The user dave is logged in on tty2 (the second virtual console), and has been on since 14:37 on 21 October. The user kurt is logged in twice—on tty3 (the third virtual console), and on ttyp1, which is an X session with a window location of (:0.0).

NOTES: This command is for listing the users on the local system; to list the users connected to a different system on the network, or to see more detailed personal information that a user may have made public, see Recipe 34.5.1 [Checking Whether a User Is Online], page 683.

## 2.6.3 Listing Who Is on and What They’re Doing

The `w` tool is similar to `who`, but it displays more detail. It outputs a header line that contains information about the current system status, including the current time, the amount of time the system has been up and running, and the number of users on the system. It then outputs a list of users currently logged in to the system, giving eight columns of information for each. These columns include username, terminal location, X session (if any), the time of login, the amount of time the user has been idle, and what command the user is running. (It also gives two columns showing the amount of time the system’s CPU has spent on all of the user’s current jobs (JCPU) and foreground processes (PCPU); processes are discussed in Recipe 2.7 [Listing Processes], page 41, and jobs in Recipe 3.3 [Managing Jobs], page 70.)

To see who is currently logged in and what they are doing, type:

```
$ w [RET]
5:27pm up 17:53, 4 users, load average: 0.12, 0.06, 0.01
USER     TTY      FROM     LOGIN    IDLE    JCPU    PCPU  WHAT
murky    tty1              Oct 20 20:09 17:22m 0.32s  0.32s -bash
dave     tty2              14:37   13.00s 2.35s  0.07s  less foo
kurt     tty3              15:04   1:00m  0.41s  0.09s  startx
kurt     ttyp1   :0.0      15:04   0:00s 21.65s 20.96s emacs
$
```

In this example, the command’s output shows that the current system time is 5:27 p.m., the system has been up for 17 hours and 53 minutes, and there are four users currently logged in: murky is logged in at tty1, has been idle for 17 hours and 22 minutes, and is at a Bash shell prompt; dave is logged in at tty2, has been idle for 13 seconds, and is using `less` to peruse a file named foo (see Recipe 9.1 [Perusing Text], page 211); and kurt is logged in at two terminals—tty3 and ttyp1, which is an X session. He ran the `startx` command on tty3 to start his X session, and within his X session, he is currently using Emacs.

## 2.6.4 Listing the Last Time a User Logged In

Use `last` to find out who has recently used the system, which terminals they used, and when they logged in and out.
