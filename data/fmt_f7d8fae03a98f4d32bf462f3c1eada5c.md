
```text
debian:/etc# dpkg -s wget
Package: wget
Status: install ok installed
Priority: optional
Section: web
Installed-Size: 558
Maintainer: Nicolás Lichtmaier <nick@debian.org>
Version: 1.5.3-3
Depends: libc6 (>= 2.1)
Conf-files:
    /etc/wgetrc  9d49747a4cb2175768db37ddd8deea36a
Description: utility to retrieve files from the WWW via HTTP and FTP
Wget [Formerly known as Geturl] is a freely available network utility
to retrieve files from the World Wide Web using HTTP and FTP, the two
most widely used Internet protocols. It works non-interactively, thus
enabling work in the background, after having logged off.

The recursive retrieval of HTML pages, as well as FTP sites is
supported -- you can use Wget to make mirrors of archives and home
pages, or traverse the web like a WWW robot (Wget understands
/robots.txt).
```

- 最后，使用 `Purge` 选项移除该软件包。例如：

```text
debian:/etc# dpkg -P wget
(Reading database ... 17030 files and directories currently installed.)
Removing wget ...
Purging configuration files for wget ...
```

### 实验 3-5 使用 `alien`

- 使用 `FTP` 从 `Red Hat` 下载一个 `RPM` 文件。下面是一个获取 `Red Hat 6.2` 中 `wget` `RPM` 的 `FTP` 会话示例。`Red Hat 7.0` 使用了更新格式的 `RPM`，而 `Debian v2.2` 默认安装的 `alien` 包尚不能识别该格式。

```text
debian:~# ftp ftp.redhat.com
Connected to ftp.redhat.com.
220 "Red Hat FTP server ready. All transfers are logged, please have a nice day."
Name (ftp.redhat.com:root): anonymous
331 Guest login ok, send your complete e-mail address as password.
Password: <Email Address>
230-Please read the file README
230- it was last modified on Tue Jan 25 08:51:37 2000 - 370 days ago
230-Please read the file README.routoughts
230- it was last modified on Fri Jan 21 17:32:20 2000 - 374 days ago
230 Guest login ok, access restrictions apply.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> cd redhat/redhat-6.2/i386/Redhat/RPMS
250 CWD command successful.
ftp> mget wget*
mget wget-1.5.3-6.i386.rpm? y
200 PORT command successful.
150 Opening BINARY mode data connection for wget-1.5.3-6.i386.rpm (153711 bytes).
226 Transfer complete.
153711 bytes received in 4.04 secs (37.2 kB/s)
ftp> quit
221-You have transferred 153711 bytes in 1 files.
221-Total traffic for this session was 156424 bytes in 2 transfers.
221-Thank you for using the FTP service on ftp.redhat.com.
221 Goodbye.
```

- 需要安装 `alien` 软件包，使用以下 `apt-get` 命令进行操作：

```text
debian:~# apt-get install alien
Reading Package Lists... Done
Building Dependency Tree... Done
The following extra packages will be installed:
  debhelper dpkg-dev file librpm1 patch rpm
The following NEW packages will be installed:
  alien debhelper dpkg-dev file librpm1 patch rpm
0 packages upgraded, 7 newly installed, 0 to remove and 45 not upgraded.
Need to get 853kB of archives. After unpacking 2126kB will be used.
Do you want to continue? [Y/n] y
Get:1 http://http.us.debian.org stable/main dpkg-dev 1.6.15 [73.7kB]
Get:2 http://http.us.debian.org stable/main file 3.28-1 [87.7kB]
Get:3 http://http.us.debian.org stable/main patch 2.5.2-2 [71.3kB]
Get:4 http://http.us.debian.org stable/main debhelper 2.0.86 [101kB]
Get:5 http://http.us.debian.org stable/main alien 6.54 [74.0kB]
Get:6 http://http.us.debian.org stable/main librpm1 3.0.3-1 [184kB]
Get:7 http://http.us.debian.org stable/main rpm 3.0.3-1 [261kB]
Fetched 853kB in 11s (72.8kB/s)
Selecting previously deselected package patch.
(Reading database ... 16992 files and directories currently installed.)
Unpacking patch (from .../patch_2.5.2-2_i386.deb) ...
Selecting previously deselected package dpkg-dev.
Unpacking dpkg-dev (from .../dpkg_1.6.15_all.deb) ...
Selecting previously deselected package file.
Unpacking file (from .../archives/file_3.28-1_i386.deb) ...
Selecting previously deselected package debhelper.
Unpacking debhelper (from .../debhelper_2.0.86_all.deb) ...
Selecting previously deselected package librpm1.
Unpacking librpm1 (from .../librpm1_3.0.3-1_i386.deb) ...
```
