Another issue: mounted NFS directories may cause problems if the remote computer fails or the connection is lost. Systems may slow down or even hang as it looks for the mounted directory.

This is where the automounter can help. It relies on the autofs daemon to mount configured directories as needed, on a temporary basis. In RHEL, the relevant configuration files are auto.master, auto.misc, auto.net, and auto.smb, all in the /etc directory. If you use the automounter, keep the /misc and /net directories free. Red Hat configures automounts on these directories by default, and they won't work if local files or directories are stored there. Subsections will cover each of these files, and a hypothetical auto.home file for automatically mounting directories from a remote server on the local /home directory.

![](bbox=[0.08, 0.44, 0.2, 0.55])

> **_You won't even see the /misc and/or /net directories unless you properly configure /etc/auto.master and the autofs daemon is running._**

Default automounter settings are configured in /etc/sysconfig/autofs. The default settings include a timeout of 300 seconds; in other words, if nothing happens on an automount within that time, the share is automatically unmounted:

```
TIMEOUT=300
```

The BROWSE_MODE can allow you to search from available mounts. The following directive disables it by default:

```
BROWSE_MODE="no"
```

There are a wide variety of additional settings available, as commented in the /etc/sysconfig/autofs file, which also assumes that the autofs daemon is active.

# /etc/auto.master

The standard /etc/auto.master file includes a series of comments, with three default commands. The first refers to the /etc/auto.misc file as the configuration file for this directory. The /net -hosts command allows you to specify the host to automount a network directory, as specified in /etc/auto.net.

```
/misc /etc/auto.misc
/net -hosts
+auto.master
```