# ### 16.2.4 Processes and Filehandles

As discussed in Chapter 10, "Getting a Handle on Files," processes can be opened in Perl via either an input or output filehandle. For example, if you want to see all the currently running processes on your machine, you can create a filehandle for the UNIX ps command. (See Chapter 10 for details. See also "The System Function" in Section 16.3.4.)

# EXAMPLE 16.32

```
(The Script)
# UNIX ps command
open(PROC, "ps -aux | ") || die "\$!\n"; # Check your UNIX man pages
# for ps options. If running on MacOS, use ps -ef
print STDOUT <PROC>;

(Output)
ellie 3825 6.4 4.5 212 464 ps R 12:18 0:00 ps -aux
root 1 0.0 0.0 52 0 ? IW Feb 5 0:02 /sbin/init
root 51 10.0 0.0 52 0 ? IW Feb 5 0:02 portmap
root 2 10.0 0.0 52 0 ? D Feb 5 0:02 psgetaemon
root 90 10.0 0.0 52 0 ? IW Feb 5 0:02 xpc.statd

<more processes here>
ellie 1383 0.8 8.4 360 876 p4 S Dec 26 11:34 /usr/local/OW3/bin/xview
ellie 173 0.8 13.4 1932 1392 co S Dec 20389:19 /usr/local/OW3/bin/xnews
ellie 164 0.0 0.0 100 0 co IW Dec 20 0:00 -c

<some of the output was cut to save space>

ellie 3822 0.0 0.0 0 p5 Z Dec 20 0:00 <defunct>
ellie 3823 0.0 1.1 28 112 ps S 12:18 0:00 sh -c ps -aux | grep '^.
ellie 3821 0.0 5.6 144 580 ps S 12:18 0:00 /usr/bin/perl checkon ellie
ellie 3824 0.0 1.8 32 192 ps S 12:18 0:00 grep '^ellie
```

# EXPLANATION

+   1. The PROC filehandle is a pipe. The output from the Linux ps command is piped to Perl via the PROC filehandle.
+   2. The contents of the filter are printed to STDOUT.