
root and place the DVD in the DVD drive. If you're using the GNOME or KDE desktop, the DVD should mount automatically. If not, type the following command to mount the DVD:

```
mount /mnt/cdrom
```

Then type the following command to change the directory:

```
cd /mnt/cdrom/RedHat/RPMS
```

This is where you find the RPM files for FTP. You can install both the FTP server and the anonymous FTP package with the following RPM commands:

```
rpm -ivh vsftpd*
```

```
rpm -ivh anonftp*
```

## Configuring the FTP Server

Red Hat Linux comes with the very secure FTP daemon (vsftpd), written by Chris Evans. The executable file for vsftpd is /usr/sbin/vsftpd, and it uses a number of configuration files in the /etc and /etc/vsftpd directories. By default, the vsftpd server is disabled; if you want to use the FTP server, first you have to enable it. In this section, I show you how.

In previous versions of Red Hat Linux, the vsftpd server was set up to run under xinetd — the Internet super server. This required editing a configuration file in /etc/xinetd.d directory to enable the vsftpd server. However, starting in Red Hat Linux 8.1, the vsftpd server is configured to run standalone, and there is an initialization script (or init script) — /etc/init.d/vsftpd — to start and stop the server. To start the vsftpd server, log in as root and type the following command:

```
service vsftpd start
```

You can also type the following command as root to turn on vsftpd so that it starts at system startup:

```
chkconfig --level 35 vsftpd on
```

After you start the vsftpd server, the default settings should be all you need to begin using the server. That's because other FTP clients can now connect and request files from your FTP server. However, you should learn about the configuration files in case you have to customize them some other time.

### vsftpd configuration files

The vsftpd server consults a number of configuration files located in the /etc and /etc/vsftpd directories. These directories control many aspects of the FTP server such as whether it runs standalone, who can download files, and whether to allow anonymous FTP. The key configuration files for vsftpd are the following:

- `/etc/vsftpd.conf` controls how the `vsftpd` server works (for example, whether it should allow anonymous logins, allow file uploads, and so on).
- `/etc/vsftpd.ftpusers` lists names of users who cannot access the FTP server.
- `/etc/vsftpd.user_list` lists names of users who are denied access (not even prompted for password). However, if the `userlist_deny` option is set to NO in `/etc/vsftpd.conf`, then these users are allowed to access the FTP server.

You can usually leave most of these configuration files with their default settings. However, just in case you have to change something to make vsftpd suit your needs, I explain the configuration files briefly in the next few sections.

### /etc/vsftpd.conf file

To find out what you can have in the /etc/vsftpd.conf file and how these lines affect the vsftpd server's operation, start by looking at the /etc/vsftpd.conf file that's installed by default in Red Hat Linux. The comments in this file tell you what each option does.

By default, vsftpd allows almost nothing. The options in /etc/vsftpd.conf loosen the restrictions so that users can use FTP. It's up to you to decide how loose the settings should be. Note that most options are set to YES. That's because most of the default settings are NO. To reverse the intent of an option, just comment out that option by placing a # at the beginning of its line.

Here are some of the options you can set in /etc/vsftpd.conf:

- `anon_mkdir_write_enable=YES` enables anonymous FTP users to create new directories. This is another risky option, and you may want to set this to NO, even if you allow anonymous users to upload files.
- `anon_upload_enable=YES` means anonymous FTP users can upload files. This option takes effect only if `write_enable` is already set to YES and the directory has write permissions for everyone. Remember that allowing anonymous users to write on your system can be very risky because someone could fill up the disk or use your disk for their personal storage.
- `anonymous_enable=YES` enables *anonymous FTP* (users can log in with the user name `anonymous` and provide their e-mail address as a password). Comment out this line if you don't want anonymous FTP.
- `ascii_download_enable=YES` enables file downloads in ASCII mode. Unfortunately, a malicious remote user can issue the SIZE command with the name of a huge file and essentially cause the FTP server to waste huge amounts of resources opening that file and determining its size. This is a typical technique used in a Denial of Service attack (which I mention later in this section).
- `ascii_upload_enable=YES` enables file uploads in ASCII mode (for text files).
- `async_abor_enable=YES` causes `vsftpd` to recognize ABOR (abort) requests that arrive at any time. You may have to enable it to allow older FTP clients to work with `vsftpd`.
- `banned_email_file=/etc/vsftpd.banned_emails` specifies the file with the list of banned e-mail addresses (used only if `deny_email_enable` is set to YES).
- `chown_uploads=YES` causes uploaded anonymous files to be owned by a different user specified by the `chown_username` option. Don't enable this option unless absolutely necessary, and don't specify `root` as the `chown_username` (that's a disaster just waiting to happen).
- `chown_username=name` specifies the user name that would own files uploaded by anonymous FTP users.
- `chroot_list_enable=YES` causes `vsftpd` to confine all users except those on a list specified by the `chroot_list_file` to their home directories when they log in for FTP service. This prevents these users from getting to any other files besides what's in their home directories.
- `chroot_list_file=/etc/vsftpd.chroot_list` is the list of users who are either confined to their home directories or not, depending on the setting of `chroot_local_user`.
- `connect_from_port_20=YES` causes `vsftpd` to make sure that data transfers occur through port 20 (the FTP data port).
- `data_connection_timeout=120` is the time in seconds after which an inactive data connection is timed out.
- `deny_email_enable=YES` causes `vsftpd` to check a list of banned e-mail addresses and deny access to anyone who tries to log in anonymously with a banned e-mail address as password.
- **dirmessage_enable=YES** causes `vsftpd` to display messages when FTP users change to certain directories.
- **ftp_banner=Welcome to my FTP service.** sets the banner that `vsftpd` displays when a user logs in. You can change the message to anything you want.
- **idle_session_timeout=600** is the time (in seconds) after which an idle session (refers to the situation where someone connects and does not do anything) times out and `vsftpd` logs the user out.
- **listen=YES** causes `vsftpd` to listen for connection requests and, consequently, run in standalone mode. Set this to NO if you want to run `vsftpd` under `xinetd`.
- **local_enable=YES** causes `vsftpd` to grant local users access to FTP.
- **local_umask=022** means whatever files FTP writes will have a permission of 644 (read access for everyone, but write access for owner only). You can set it to any file permission mask setting you want. For example, if you want no permissions for anyone but the owner, change this to 077.
- **ls_recurse_enable=YES** enables FTP users to recursively traverse directories by using the `ls -R` command.
- **nopriv_user=ftp** identifies an unprivileged user account that the FTP server can use.
- **pam_service_name=vsftpd** is the name of the Pluggable Authentication Module (PAM) configuration file that is used when `vsftpd` must authenticate a user. By default the PAM configuration files are in `/etc/pam.d` directory. That means the `vsftpd` PAM configuration file is `/etc/pam.d/vsftpd`.
- **tcp_wrappers=YES** enables support for access control through TCP wrapper that consults the files `/etc/hosts.allow` and `/etc/hosts.deny` (for more information about TCP wrapper, see Book VII, Chapter 3).
- **userlist_deny=YES** causes `vsftpd` to deny access to the users listed in the `/etc/vsftpd.user_list` file. These users are not even prompted for a password.
- **write_enable=YES** causes `vsftpd` to allow file uploads to the host.
- **xferlog_enable=YES** turns on the logging of file downloads and uploads (always a good idea, but takes disk space).
- **xferlog_file=/var/log/vsftpd.log** specifies the full pathname of the `vsftpd` log file. The default is `/var/log/vsftpd.log`.
- **xferlog_std_format=YES** causes `vsftpd` to generate log files in a standard format used by other FTP daemons.
