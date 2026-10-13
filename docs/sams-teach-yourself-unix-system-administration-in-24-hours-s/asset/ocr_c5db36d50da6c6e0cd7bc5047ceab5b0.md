```
# shutdown -c
Shutdown cancelled.
[1]+ Done          shutdown -r 05:00
```

4. This leads to the question about whether you should ever use halt or reboot. On modern Linux systems, they turn out to be links to shutdown, so it's not an issue, but other Unix systems allow system administrators to directly halt or reboot their system, without warning, and without any of the graceful termination of services that shutdown offers.

For example, Mac OS X offers shutdown, which is completely flag-for-flag compatible with Linux, but the halt and reboot commands are also available.

However, the halt man page gently reminds admins:

> > Normally, the shutdown(8) utility is used when the system needs to be halted or restarted, giving users advance warning of their impending doom.

Solaris has a rather different version of shutdown, with only three flags allowed: -y, -g graceperiod, and -i initstate. Furthermore, you specify the grace period time with the -g flag, rather than as a regular parameter. So a standard reboot command for Solaris, offering a five minute grace period, is

```
# /usr/bin/shutdown -y -g 300 -i6
```

By default, Solaris shutdown drops you into single-user (init level 1) mode. Therefore, to halt the machine, you'll want to use -i0, and to reboot, you'll use -i6.

![](bbox=[0.22, 0.7, 0.28, 0.8])

> As a general rule of thumb, use shutdown regardless of your operating system, and always try to give users at least 60 seconds grace period, if possible.

5. One final note: The -k flag offers some interesting capabilities. On Linux, for example, you can use it to practice working with shutdown because it causes the program to send the shutdown warning, but doesn't actually do the shutdown requested.

Mac OS X is even cooler: The -k flag kicks everybody off the system, and prevents subsequent logins from other than the console. It leaves the system in multi-user mode with all the services running, and does not halt/reboot.

There are often times when you want to reboot the system, and sporadically you'll want to halt it completely (perhaps to upgrade the hardware, or to move the server to a new physical location). Regardless, always use shutdown for these tasks.