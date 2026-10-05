kppp displays the message 'pppd died unexpectedly,' there are highly probable reasons for this: either /etc/ppp/options is missing completely, or /etc/ppp/options or "/.pprc contains the keyword lock. (This means that pppd is responsible for locking. Most of the time, this makes sense, but not in connection with kppp, which takes on this task by itself. Delete lock!) In case of doubt, simply go with a completely empty /etc/ppp/options file. Please also read the excellent online documentation!

kppp is usually installed as a SETUID program. This means that it has root privileges irrespective of who is executing it. Although this is a security risk (the documentation explains how it can be filled), it has one great advantage: in contrast to other scripts introduced in this chapter, it can be used by all users (not by root) without any significant problems. The only prerequisite is that all users are allowed to execute pppd. This is achieved by the the following command:

```
root# chmod +x /usr/sbin/pppd
```

# Linuxconf (RedHat)

In the hierarchical menu of Linuxconf, the PPP configuration is hidden under SETTINGS|NETWORK|PPP. With the new button, you create the new PPP device pp0. In the Interface dialog, you must enter the phone number, serial interface, login name, and password. If you want to carve out with PAP (usually the simplest alternative), you must activate the appropriate option - it is not enabled in the default setting.

![](bbox=[0.268, 0.513, 0.8, 0.793])

Figure 9.4 PPP configuration with Linuxconf.

CONFIRM takes you back to the main dialog. By clicking on the interface name pp0, you get into a new dialog with further configuration options. You can set here the speed of the serial interface and various pppd parameters.