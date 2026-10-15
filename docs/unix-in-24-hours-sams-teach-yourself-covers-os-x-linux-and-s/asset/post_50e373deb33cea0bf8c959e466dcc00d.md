
david mark taylor
%

In this example, david and mark are also logged in to the system with me. Try this on your computer and see what other users—if any—are logged in to your computer system.

- 2. A command that you’ve encountered earlier in this hour can be used to find out who is logged on to the system, what line they’re on, and how long they’ve been logged in. That command is who:

Click here to view code image

```
% who
 taylor    vt/7      Oct 27 14:10   (:0)
 david     pts/1      Dec 27 15:54   (:0.0)
 mark      pts/2      Oct 27 11:51   (:0.0)
%
```

Here, you can see that three people are logged in: taylor (me), david, and mark. Furthermore, you can now see that david is logged in by connection pts/1 and has been connected since December 27 at 3:54 p.m. You can see that mark has been connected since just before noon on October 27 on line pts/2. Note that I have been logged in since 14:10, which is 24-hour time for 2:10 p.m. Unix doesn’t always indicate a.m. or p.m.

The user and who commands can tell you who is using the system at any particular moment, but how do you find out what they’re doing?

## Task 2.6: What Is Everyone Doing on the Computer?

To find out what everyone else is doing, there’s a third command, w, that serves as a combination of “Who are they?” and “What are they doing?”

- 1. Consider the following output from the w command:

Click here to view code image

```
% w
2:12pm  up 7 days,   5:28,  3 users,  load average: 0.33, 0.33, 0.02
User     tty      login@   idle   JCPU   PCPU  what
taylor   vt/7     27Oct14  2:35   2:07   python2.6
/usr/lib/system-config
david    pts/1    3:54pm   2:04   15     33     bash
mark     pts/2    27Oct14  43            -csh
%
```

In this example, the current time is 2:12 p.m., and the system has been up for 7 days, 5 hours, and 28 minutes. Currently three users are logged in, and the system is very quiet, with an average of 0.33 jobs submitted (or programs started) in the last minute; 0.33 jobs, on average, in the last 5 minutes; and 0.02 jobs in the last 15 minutes.

taylor is the only user actively using the computer (that is, who has no idle time) and is using the python command. User david is sitting in the bash shell, which has gone for quite awhile without any input from the user (2 hours and 11 minutes of idle time). The program already has used 15 seconds of CPU time and, overall, david has used 33 seconds of CPU time. User mark has a C shell running, as indicated by -csh. (The leading dash indicates that this is the program that the computer launched automatically when mark logged in. This is akin to how the system automatically launches the Finder on a Macintosh.) User mark hasn’t actually done anything yet: Notice that there is no accumulated computer time for that account.

- 2. Now it’s your turn. Try the w command on your system and see what kind of output you get. Try to interpret all the information based on the explanation here. One thing is certain: Your account should have the w command listed as what you’re doing.

On a multiuser Unix system, the w command gives you a quick and easy way to see what’s going on.

## Task 2.7: Checking the Current Date and Time

You’ve learned how to orient yourself on a Unix system, and you are now able to figure out who you are, who else is on the system, and what everyone is doing. What about the current time and date?

- 1. Logic suggests that time shows the current time and date the current date; but this is Unix, and logic doesn’t always apply. In fact, consider what happens when I enter time on my system:

```
$ time

real    0m0.000s
user    0m0.000s
sys     0m0.000s
$
```

The output is cryptic to the extreme and definitely not what you’re interested in finding out. The program is showing how much user time, system time, and CPU time has been used by the command interpreter itself, broken down by input/output operations and more. (The time command is more useful than it looks, particularly if you’re a programmer.)

On other Unixes, you might find time to be a missing command, a built-in shell function, or something completely different. In all cases, it won’t tell you the current time.
