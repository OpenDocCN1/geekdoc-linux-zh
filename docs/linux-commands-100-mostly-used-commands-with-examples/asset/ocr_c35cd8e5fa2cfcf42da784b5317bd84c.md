Use a text editor like `nano` to edit the static host name in the `/etc/hostname` file. After editing, save the changes and exit the editor.

+   7. **Edit the hosts file to associate the host name with an IP address:**

```
sudo nano /etc/hosts
```

The `/etc/hosts` file maps IP addresses to host names. You can edit this file to associate your host name with the desired IP address.

+   8. **Check the current domain name:**

```
domainname
```

This command displays the NIS/YP domain name associated with the system.

# **74. zip: Package and compress files.**

The `zip` command in Linux is used for compressing files and directories into a zip archive. It is a popular utility for creating and managing compressed files in a cross-platform manner.

**Examples:**

+   1. **Zip a Single File:**