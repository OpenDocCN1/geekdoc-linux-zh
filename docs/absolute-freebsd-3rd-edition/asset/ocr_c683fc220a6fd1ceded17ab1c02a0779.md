```
# chmod 777 /var/tftproot/programname
```

Yes, this means that anyone who knows a file’s name can overwrite the contents of that file. Make vital files read-only. ${ }^{8}$ This also means you don’t have to worry about someone uploading a big file and filling your hard drive.

# File Ownership

Files in a TFTP server should be owned by a user with the least possible privilege. If you run a TFTP server only intermittently, you can use the nobody user. For example, if you need the TFTP server only to perform the occasional embedded device upgrade, let the nobody user own your files and just turn tftpd(8) off when it’s not needed. If you run a permanent TFTP server, however, it’s best to have a dedicated tftp unprivileged user to own the files. The tftp user doesn’t need to own the tftp_root directory and, in fact, should have an entirely different home directory. He needs ownership only of the files available to users.

# tftpd(8) Configuration

tftpd(8) is configured entirely through command line arguments, and there aren’t many of them. For a full list, read tftpd(8), but here are the most commonly used ones.

If you create a user just to run tftpd(8), specify that user with the -u argument. If you don’t specify a user, tftpd(8) runs as nobody. Create an unprivileged user.

I recommend logging all requests to your TFTP daemon. The -1 argument turns on logging. tftpd(8) uses the FTP facility, which you must enable in syslog.conf (see Chapter 21).

Tftpd supports chrooting with the -s flag. This lets you confine tftpd(8) to your selected directory. You don’t want users to TFTP world-readable files such as /etc/passwd, or even /boot/kernel/kernel, just on general principle! Always chroot your tftpd(8) installation.