
For systems where iconv() is not available or where iconv()’s locales are not compatible with Windows, UTF-8 is the only locale available.

There are no systems that use UTF-8 as the default locale for Japanese.

Some broken filenames may be displayed, and some commands that cannot handle non-ASCII filenames may be aborted during parsing filenames. Especially, there may be `\` (\(0xfc)) in filenames, which must be handled carefully, so you had better not touch filenames written from Windows on UNIX.

In addition, although it is not directly concerned with Samba, since there is a delicate difference between the iconv() function, which is generally used on UNIX, and the functions used on other platforms, such as Windows and Java, so far as concerns the conversion between Shift_JIS and Unicode UTF-8 must be done with care and recognition of the limitations involved in the process.

Although Mac OS X uses UTF-8 as its encoding method for filenames, it uses an extended UTF-8 specification that Samba cannot handle, so UTF-8 locale is not available for Mac OS X.

## Shift_JIS series + vfs_cap (CAP encoding)

CAP encoding means a specification used in CAP and NetAtalk, file server software for Macintosh. In the case of CAP encoding, for example, if a Japanese filename consists of 0x8baa and 0x9f4c, and “txt” is written from Windows on Samba, the filename on UNIX becomes “:8baa:9f4c.txt” (a 14 bytes ASCII string).

For CAP encoding, a byte that cannot be expressed as an ASCII character (0x80 or above) is encoded in an “:xx” form. You need to take care of containing a `\` (\(0x5c)) in a filename, but filenames are not broken in a system that cannot handle non-ASCII filenames.

The greatest merit of CAP encoding is the compatibility of encoding filenames with CAP or NetAtalk. These are respectively the Columbia Appletalk Protocol, and the NetAtalk Open Source software project. Since those software applications write a file name on UNIX with CAP encoding, if a directory is shared with both Samba and NetAtalk, you need to use CAP encoding to avoid non-ASCII filenames from being broken.

However, recently, NetAtalk has been patched on some systems to write filenames with EUC-JP (e.g., Japanese original Vine Linux). In this case, you need to choose EUC-JP series instead of CAP encoding.

vfs_cap itself is available for non-Shift_JIS series locales for systems that cannot handle non-ASCII characters or systems that share files with NetAtalk.

To use CAP encoding on Samba-3, you should use the unix charset parameter and VFS as in Example 29.5.1.

You should set CNF42 if using GNU libiconv for unix charset. With this setting, filenames in the “cap-share” share are written with CAP encoding.

### Example 29.5.1 VFS CAP

```
[global]
# the locale name "CP932" may be different
    dos charset = CP932
    unix charset = CP932
[cap-share]
    vfs option = cap
```

### 29.5.2 Individual Implementations

Here is some additional information regarding individual implementations:

**GNU libiconv** To handle Japanese correctly, you should apply the patch libiconv-1.8-cp932-patch.diff.gz⁴ to libiconv-1.8.

Using the patched libiconv-1.8, these settings are available:

![](img/86d74c6cc862465e3a42e6dc3c90935a_585_0.png)

Other Japanese locales (for example, Shift_JIS and EUC-JP) should not be used because of the lack of the compatibility with Windows.

**GNU glibc** To handle Japanese correctly, you should apply a patch⁵ to glibc-2.2.5/2.3.1/2.3.2 or should use the patch-merged versions, glibc-2.3.3 or later.

Using the above glibc, these setting are available:

```
  dos charset = CP932
  unix charset = CP932 / eucJP-ms / UTF-8
  display charset = CP932
```

Other Japanese locales (for example, Shift_JIS and EUC-JP) should not be used because of the lack of the compatibility with Windows.

### 29.5.3 Migration from Samba-2.2 Series

Prior to Samba-2.2 series, the “coding system” parameter was used. The default codepage in Samba 2.x was code page 850. In the Samba-3 series this has been replaced with the **unix charset** parameter. Table 29.1 shows the mapping table when migrating from the Samba-2.2 series to Samba-3.

Table 29.1 Japanese Character Sets in Samba-2.2 and Samba-3

| Samba-2.2 Coding System | Samba-3 unix charset |
| :---: | :---: |
| SJIS | Shift_JIS series |
| EUC | EUC-JP series |
| EUC3⁽ᵃ⁾ | EUC-JP series |
| CAP | Shift_JIS series + VFS |
| HEX | currently none |
| UTF8 | UTF-8 |
| UTF8-Mac⁽ᵇ⁾ | currently none |
| others | none |

⁽ᵃ⁾Only exists in Japanese Samba version
⁽ᵇ⁾Only exists in Japanese Samba version

## 29.6 Common Errors

### 29.6.1 CP850.so Can’t Be Found

“Samba is complaining about a missing **CP850.so** file.”

**CP850** is the default **dos charset**. The **dos charset** is used to convert data to the codepage used by your DOS clients. If you do not have any DOS clients, you can safely ignore this message.

**CP850** should be supported by your local iconv implementation. Make sure you have all the required packages installed. If you compiled Samba from source, make sure that the configure process found iconv. This can be confirmed by checking the **config.log** file that is generated when **configure** is executed.

# Chapter 30

## BACKUP TECHNIQUES

### 30.1 Features and Benefits

The Samba project is over 10 years old. During the early history of Samba, UNIX administrators were its key implementors. UNIX administrators use UNIX system tools to backup UNIX system files. Over the past 4 years, an increasing number of Microsoft network administrators have taken an interest in Samba. This is reflected in the questions about backup in general on the Samba mailing lists.

### 30.2 Discussion of Backup Solutions

During discussions at a Microsoft Windows training course, one of the pro-UNIX delegates stunned the class when he pointed out that Windows NT4 is limiting compared with UNIX. He likened UNIX to a Meccano set that has an unlimited number of tools that are simple, efficient, and, in combination, capable of achieving any desired outcome.

One of the Windows networking advocates retorted that if she wanted a Meccano set, she would buy one. She made it clear that a complex single tool that does more than is needed but does it with a clear purpose and intent is preferred by some like her.

Please note that all information here is provided as is and without recommendation of fitness or suitability. The network administrator is strongly encouraged to perform due diligence research before implementing any backup solution, whether free software or commercial.

A useful Web site I recently stumbled across that you might like to refer to is located at www.allmerchants.com$^{1}.$

The following three free software projects might also merit consideration.

$^{1}$<http://www.allmerchants.com/Software/Backup-Software/>  
$^{2}$<http://backuppc.sourceforge.net>

#### 30.2.1 BackupPC

BackupPC version 2.0.0 has been released on SourceForge$^{2}$. New features include support for **rsync**/**rsyncd** and internationalization of the CGI interface (including English, French, Spanish, and German).

BackupPC is a high-performance Perl-based package for backing up Linux, UNIX, and Windows PCs and laptops to a server's disk. BackupPC is highly configurable and easy to install and maintain. SMB (via smclient), tar over rsh/ssh, or rsync/rsyncd are used to extract client data.

Given the ever-decreasing cost of disks and RAID systems, it is now practical and cost effective to backup a large number of machines onto a server's local disk or network storage. This is what BackupPC does.

Key features are pooling of identical files (big savings in server disk space), compression, and a comprehensive CGI interface that allows users to browse backups and restore files.

BackupPC is free software distributed under a GNU GPL licence. BackupPC runs on Linux/UNIX/freeunix servers and has been tested on Linux, UNIX, Windows 9x/Me, Windows 98, Windows 200x, Windows XP, and Mac OS X clients.

#### 30.2.2 rsync

rsync is a flexible program for efficiently copying files or directory trees.

rsync has many options to select which files will be copied and how they are to be transferred. It may be used as an alternative to ftp, http, scp, or rcp.

The rsync remote-update protocol allows rsync to transfer just the differences between two sets of files across the network link, using an efficient checksum-search algorithm described in the technical report that accompanies the rsync package.

Some of the additional features of rsync are:

- Support for copying links, devices, owners, groups, and permissions.
- Exclude and exclude-from options are similar to GNU tar.
- A CVS exclude mode for ignoring the same files that CVS would ignore.
- Can use any transparent remote shell, including rsh or ssh.
- Does not require root privileges.
- Pipelining of file transfers to minimize latency costs.
- Support for anonymous or authenticated rsync servers (ideal for mirroring).

#### 30.2.3 Amanda

Amanda, the Advanced Maryland Automatic Network Disk Archiver, is a backup system that allows the administrator of a LAN to set up a single master backup server to back up multiple hosts to a single large capacity tape drive. Amanda uses native dump and/or GNU tar facilities and can back up a large number of workstations running multiple versions of UNIX. Recent versions can also use Samba to back up Microsoft Windows hosts.
