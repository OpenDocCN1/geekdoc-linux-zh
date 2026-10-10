remote1. The following steps show how to run an X application from remote1 from your X display on local1.

> **CAUTION:** This procedure assumes that no special security procedures are implemented. It is the default situation and is designed for sharing applications among trusted computers (usually single-user workstations) on a local network. This method is inherently insecure and requires that you trust all users on computers to which you allow access. If you require a more secure method, refer to the section “Using SSH to run remote X applications” later in this chapter.

You may need to enable your X server to support networked connections. To see if you need to enable networked connections, run the following command:

```
$ ps aux | grep Xorg
root      1941  0.0  2.1  54276 44972 tty1   Ss+  11:14   0:04
/usr/bin/Xorg :0 -nr -verbose -auth /var/run/gdm/auth-for-gdm-D98Kms/database vt1 -nolisten tcp
ericfj    6034  0.0  0.0   4212   724 pts/0  R+   12:21   0:00 grep Xorg
```

If you see -nolisten tcp in the Xorg command, you need to enable networked connections. To do so, edit the file /etc/gdm/gdm.schemas if you are using the GNOME display manager, the Fedora default. Look for the following block in this XML file:

```
<schema>
    <key>security/DisallowTCP</key>
    <signature>bx</signature>
    <default>true</default>
</schema>
```

Change this setting to the following:

```
<schema>
    <key>security/DisallowTCP</key>
    <signature>bx</signature>
    <default>false</default>
</schema>
```

After this, restart your system. Log in and make sure the -nolisten tcp argument is no longer present:

```
$ ps aux | grep Xorg
root      2141  0.0  2.1  54276 44972 tty1   Ss+  12:04   0:04
/usr/bin/Xorg :0 -nr -verbose -auth /var/run/gdm/auth-for-gdm-e2VZ7d/database vt1
```

Once completed, follow these steps to enable remote applications to connect to your desktop:

+   1. Open a Terminal window on the local computer.