
```
[root@redhat /root]# ftp ftp.redhat.com
Connected to ftp.redhat.com.
220 "Red Hat FTP server ready. All transfers are logged,
please have a nice day."
Name (ftp.redhat,com:root): anonymous
331 Guest login ok, send your complete e-mail address as password.
Password: <Email_Address>
230-Please read the file README
230- it was last modified on Tue Jan 25 08:51:37 2000 - 369 days ago
230-Please read the file README.roughcuts
230- it was last modified on Fri Jan 21 17:32:20 2000 - 373 days ago
230 Guest login ok. access restrictions apply.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> cd redhat/current/i386/00
250-Please read the file README
250- it was last modified on Fri Aug 25 12:31:19 2000 - 156 days ago
250 CWD command successful.
ftp> get RPM-GPG-KEY
local: RPM-GPG-KEY remote: RPM-GPG-KEY
200 PORT command successful.
150 Opening BINARY mode data connection for RPM-GPG-KEY (1908 bytes).
226 Transfer complete.
1908 bytes received in 0.0589 secs (32 Kbytes/sec)
ftp> cd RedHat/RPMS
250 CWD command successful.
ftp> mget wget* lynx*
ftp> wget-1.5.3-10.i386.rpm? y
200 PORT command successful.
150 Opening BINARY mode data connection for wget-1.5.3-10.i386.rpm (156532 bytes).
226 Transfer complete.
156532 bytes received in 0.948 secs (1.6e+02 Kbytes/sec)
ftp> lynx-2.8.4-3.i386.rpm? y
200 PORT command successful.
150 Opening BINARY mode data connection for lynx-2.8.4-3.i386.rpm (935337 bytes).
226 Transfer complete.
935337 bytes received in 5.29 secs (1.7e+02 Kbytes/sec)
ftp> quit
221-You have transferred 1250309 bytes in 4 files.
221-Total traffic for this session was 1253244 bytes in 7 transfers.
221-Thank you for using the FTP service on pub.nyc.redhat.com.
221 Goodbye.
```

使用以下命令将 Red Hat 公钥文件导入 `gpg`（如果是第一次运行 `gpg`，你需要执行两次）：

```
[root@redhat /root]# gpg --import RPM-GPG-KEY
gpg: /root/.gnupg: directory created
gpg: /root/.gnupg/options: new options file created
```

### Debian 实验室

这些实验应在基于 Debian 的系统上完成。

以下是新安装 Debian 系统中默认的 `/etc/apt/sources.list` 示例。你将在后续实验中使用它。

```text
# See sources.list(5) for more information, especially
# Remember that you can only use http, ftp or file URLs
# CDROMs are managed through the apt-cdrom tool.
#deb http://http.us.debian.org/debian stable main contrib non-free
#deb http://non-us.debian.org/debian-non-US stable/non-US main contrib non-free
#deb http://security.debian.org stable/updates main contrib non-free

# Uncomment if you want the apt-get source function to work
#deb-src http://http.us.debian.org/debian stable main contrib non-free
#deb-src http://non-us.debian.org/debian-non-US stable non-US

deb cdrom:[Debian GNU/Linux 2.2 r0 _Potato_ - Official 1386 Binary-1 (20000814)]
/ unstable contrib main non-US/contrib non-US/main
```

#### 实验 3-4 使用 Debian 软件包

1. 移除 `sources.list` 文件中前三个源行的注释。例如：

   ```text
   deb http://http.us.debian.org/debian stable main contrib non-free
   deb http://non-us.debian.org/debian-non-US stable/non-US main contrib non-free
   deb http://security.debian.org stable/updates main contrib non-free
   ```

2. 执行 `apt-get update` 以从 Debian 软件包站点刷新可用软件包列表。
