**TABLE 27.1 CONTINUED**

| Filename | Description |
|---|---|
| `ftpaccess` | The `ftpaccess` file is used to define user classes, based on the account accessed and the host from which the user connects. You can also deny access to a certain class of users or limit their number of connections during specific times of the week in this file, as well as specify who has permission to perform particular actions such as directory creation and file uploading. |
| `ftpusers` | Usernames listed in the `ftpusers` file are not allowed access to the FTP server. |
| `ftpservers` | The `ftpservers` file allows you to implement support for FTP Virtual domains. Through this file, you can specify different sets of configuration files for different virtual servers that can be distinguished by their IP addresses or their virtual domain names. |
| `ftpgroups` | The `ftpgroups` file provides support for FTP site groups and FTP site passwords. |

The use of these files is discussed within the context of various tasks throughout this chapter.

# BUILDING WU-FTPD FROM SOURCE

Generally, WU-FTPD comes with most Linux distributions as pre-built binary packages. Accordingly, building WU-FTPD from source code is not necessary. However, if you want to upgrade to a newer version of WU-FTPD before a binary package becomes available for your distribution or if your distribution includes a different FTP server and you want to use WU-FTPD, then you might need to build WU-FTPD from source.

The source code for WU-FTPD is available online at `ftp://ftp.wu-ftpd.org/`. The current version of the software is 2.6 and is available at `ftp://ftp.wu-ftpd.org/pub/wu-ftpd/wu-ftpd-2.6.tar.gz`.

> > **Tip**
> > The latest stable release might have changed by the time you download the software, but you should always use the latest stable version to be sure that you have the latest security and bug fixes.

You can unpack and build WU-FTPD as follows:

+   1. Download the archive to a convenient location such as `/tmp/`.
+   2. Unpack the source in a suitable place, where you keep all software source code, for example, `/usr/local/src/` or `/opt/src/`. To unpack the archive in `/usr/local/src/`, use the following commands:

```
```bash
# cd /usr/local/src/
# tar zxvf /tmp/wu-ftpd-2.6.tar.gz
```
```