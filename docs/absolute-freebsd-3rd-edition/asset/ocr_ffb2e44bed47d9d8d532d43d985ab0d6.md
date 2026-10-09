```
ADMIN$ disk Remote Admin
C$ disk Default share
unix disk
4 shares listed from 4 available
```

You’ll get a list of every shared resource on the CIFS server. Now, assuming you’re finished, log out of the server.

```
# smbutil logout //unix@fileserver
```

# Mounting a Share

Now that you’ve finished investigating, mount a share with mount_smbfs(8). The syntax is as follows:

```
# mount_smbfs //username@servername/share /mount/point
```

I have a share on this Windows box called *MP3* that I want to access from my FreeBSD system. To mount this as /home/mwlucas/smbmount, I would do this:

```
# mount_smbfs //unix@fileserver1/MP3 /home/mwlucas/smbmount
```

The mount(8) and df(1) programs show this share attached to your system, and you can access documents on this server just as you could any other filesystem. Use umount(8) to disconnect from the server.

# Other mount_smbfs Options

mount_smbfs includes several options to tweak the behavior of mounted CIFS filesystems. Use the `-f` option to choose a different file permission mode and the `-d` option to choose a different directory permission mode. For example, to set a mount so that only I could access the contents of the directory, I would use `mount_smbfs -d 700`. This would make the FreeBSD permissions far more stringent than the Windows privileges, but that’s perfectly all right with me. I can change the owner of the files with the `-u` option and the group with the `-g` option.