```
david mark taylor
%
```

In this example, david and mark are also logged in to the system with me. Try this on your computer and see what other users—if any—are logged in to your computer system.

+   2. A command that you’ve encountered earlier in this hour can be used to find out who is logged on to the system, what line they’re on, and how long they’ve been logged in. That command is who:

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

# Task 2.6: What Is Everyone Doing on the Computer?

To find out what everyone else is doing, there’s a third command, w, that serves as a combination of “Who are they?” and “What are they doing?”

+   1. Consider the following output from the w command:

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