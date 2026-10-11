![](bbox=[0.1, 0.08, 0.78, 0.2])

Figure 18. Editing the Red Hat Network sources file as superuser.

In the sources file, search for the line that says

```
yum updates-released http://fedora.redhat.com/updates/released/fedora-core-1
```

Although the first word is "yum," this works for both up2date and yum. Replace it with a line like so (this line wraps onto two lines for publication in this document):

```
yum updates-released
http://www.glilb.cc.gatech.edu/pub/fedora.redhat/linux/core/updates/1/i386
```

You'll note that there are two other lines, one that says

```
yum fedora-core-1 http://fedora.redhat.com/releases/fedora-core-1
```

and another that says

```
yum updates-testing http://fedora.redhat.com/updates/testing/fedora-core-1
```

You can make similar changes to these lines if you're interested in changing the servers for the core files and for the testing updates files.

In either case, save the file, and you're ready to launch up2date.

# Launch up2date

up2date is the actual mechanism that goes to the mirror site, fetches files, and installs them on your machine, all in one handy interface.

Click the "Launch up2date" menu option from the Red Hat Network Alert Notification Tool. You'll be greeted with the dialog in Figure 19 that requests you to log in as root.

Upon successful login, you'll be greeted with the Welcome screen to the Red Hat Update Agent wizard, as shown in Figure 20.

![](bbox=[0.1, 0.79, 0.5, 0.93])

Figure 19. First, log in as root in order to run up2date.