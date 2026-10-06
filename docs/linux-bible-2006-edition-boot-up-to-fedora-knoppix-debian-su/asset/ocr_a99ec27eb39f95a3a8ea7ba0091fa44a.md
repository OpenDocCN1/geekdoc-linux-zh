The Fedora Setup Agent runs automatically only if you have configured Fedora to boot to a graphical login prompt. To start it from a text login, log in as root and switch to init state 5 temporarily (type **init 5**). Log in to the graphical prompt. By a Terminal window, as root user,

```
# rm /etc/sysconfig/firstboot
# /usr/sbin/firstboot
```

The Welcome screen displays. From it, step through screens to configure date and time, your monitor, user accounts, and additional software.

# Summary

After throwing its devoted following into turmoil by dropping the well-known Red Hat Linux name. Red Hat, Inc. focused its development efforts into the free Fedora Project and commercial Red Hat Enterprise Linux.

Fedora Core and Red Hat Enterprise Linux distributions distinguish themselves from other Linux distributions with their simplified installer (called Anaconda), graphical configuration tools, and RPM Package Management tools. Fedora Core is freely available, whereas Red Hat Enterprise Linux is available on a paid subscription basis.

Fedora Core is included on the DVD that comes with this book. You can install the complete Fedora Core distribution by following the detailed instructions included in this chapter.