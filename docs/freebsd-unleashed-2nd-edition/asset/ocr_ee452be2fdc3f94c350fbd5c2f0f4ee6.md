+   * `/var/ftp/etc/passwd` and `/var/ftp/etc/group`—As with the tools in `/var/ftp/bin`, these are copies of the default `/etc/passwd` and `/etc/group` files, whose purpose is to provide file ownership mappings during directory listings. Because anonymous FTP access is limited to what’s in `/var/ftp`, these files must exist in order to show who owns the various files in `/var/ftp`. Typically, any files in the public FTP area will be owned by root or another system account because they will be put there by you, as the administrator. Other usernames, because they don’t exist in `/var/ftp/etc/passwd`, will not be mapped and will appear to FTP users as raw UIDs for files owned by them.

+   * `/var/ftp/etc/ftpmotd`—Operates the same way as `/etc/ftpmotd`, except that this one is displayed to anonymous FTP users instead of regular login users. From their perspective (with the chroot making `/var/ftp` appear to be `/` to them), this is `/etc/ftpmotd`.

+   * `/var/ftp/pub`—Visible to any anonymous FTP users as `/pub`, this is where all downloadable files should go. The hierarchy under `/pub` is up to you to determine, but convention says at least that `/pub` should contain everything that’s meant to be of interest to the public.

+   * `/var/ftp/incoming`—This optional directory has world-writable permissions with the “sticky bit” set (1777). This means that any anonymous user can upload files into this directory. This can be dangerous; having an open upload directory is an invitation for people to use it as a trading point for MP3 files and pirated software. Use this option only if you really need to!

One final configuration file that concerns the FTP server is `/etc/inetd.conf`. As mentioned earlier, ftpd runs as a subsidiary to the inetd super-server, and as such it won’t work if inetd isn’t running. First, use ps to check to see whether the daemon is serving requests, using the -w (wide format), -a (all users’ processes), -u (user-oriented fields shown), and -x (processes that aren’t necessarily attached to terminals) options:

```
```
# ps -aux | grep inetd
root  1640 0.0 0.6 1048 780 ?? Ss Thu08PM 0:00.15 inetd -Ww
```
```

If you don’t see the inetd process running, you may have turned it off in `/etc/rc.conf`; check there for the inetd_enable="NO" line and remove or disable it if it’s present. Second, open up `/etc/inetd.conf` and make sure the ftpd service is enabled:

```
```
ftp stream tcp nowait root /usr/libexec/ftpd ftpd -l
```
```

If this line is commented out, uncomment it, and restart inetd (using the killall -HUP inetd command). Check your configuration by trying to connect to the server (ftp localhost). If you are presented with a login prompt, you’re in business. If not, look over the preceding steps again; kill inetd completely and restart it if necessary.