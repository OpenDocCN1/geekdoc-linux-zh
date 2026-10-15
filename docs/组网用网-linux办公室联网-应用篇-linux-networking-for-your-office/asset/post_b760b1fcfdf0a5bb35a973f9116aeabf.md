
Of course Table 11.2 only scratches the surface of the possibilities. In a network with many users and groups interacting in complex ways, you might have several different shared directories with differing permissions for assorted groups of users. These options also interact with some of the share availability options discussed earlier in the chapter. In general, actual access is determined by the most restrictive options specified. Fortunately, most small networks can do quite well with just a few simple options.

## Filename Case and Mangling Options

Linux is a case-sensitive OS (p. 230), whereas Windows is a case-retentive OS (p. 230). In addition, Linux supports longer filenames than Windows, and much longer filenames than DOS. Also, DOS is a case-insensitive OS (p. 230), which adds yet more complications to the mix.

Samba’s default behavior is to take great pains to conform to the client OS’s expectations for filename case and length. In some situations, particularly when dealing with DOS clients, Samba must mangle a name, or shorten it in such a way that Samba can still match the on-disk filename to the one used by the client. If you’ve used Windows 95 or later, you’re probably familiar with name mangling as performed on FAT/VFAT filesystems because VFAT includes built-in name mangling capabilities. This is demonstrated by a directory listing in a Windows command prompt window, like this:

```
A:\>dir
Volume in drive A is FLOPPY
Directory of A:\
FILE1 TXT        99 10-05-99  2:19p FILE1.TXT
LONGFI~1.TXT     99 10-05-99  2:21p LongFilename.txt

               5 file(s)           198 bytes
```

The file called LongFilename.txt also bears the mangled filename LONGFI~1.TXT, which is used by DOS and older Windows programs that don’t understand long filenames. Samba supports a similar feature, even on filesystems that don’t include explicit support for name mangling.

### NOTE

> In Windows, the VFAT and NTFS filesystems provide direct support for name mangling. Even when using VFAT or NTFS, though, Samba’s name mangling is self-generated. Therefore, you don’t see the same mangled names in a Samba share that you see when accessing the same FAT or NTFS disk directly or from a Windows server. If you dual-boot a server between Linux and Windows, DOS clients therefore see different filenames for non-8.3-compliant names.

Samba options that affect name mangling and case-sensitivity include the following:

- **mangled names**—The default for this option is yes. If you set this option to no, Samba doesn't perform name mangling; it simply truncates filenames, which can result in two files having the same name. When this happens, you can access only one file.
- **mangle case**—Converts the case of files, normally providing all-uppercase names to the clients. The default is no.
- **case sensitive**—If this option is set to yes, Samba treats filenames in a case-sensitive manner. The default is no, which requires that Samba do more work to match filenames.
- **default case**—This option specifies the default case for new files from case-insensitive clients. The default is lower.
- **preserve case**—If this option is set to yes (the default), it preserves case from case-retentive OSs, such as Windows and OS/2. If it is set to no, filenames are converted to the default case.

## The Samba Daemons

Like most networking services, Samba operates by running daemons (p. 62). The Samba package contains two daemons:

- **smbd**—The SMB daemon provides the bulk of the services you think of when you think of Windows networking, including the all-important file-exchange services.
- **nmbd**—The name browser daemon is responsible for announcing the presence of your Linux server on the NetBIOS network. If it's not configured properly, you can't access your Linux computer's shares from Windows.

There are two ways to run the Samba daemons: independently and from inetd. Each has advantages and disadvantages.

## Running Samba Independently

If you type ps ax | grep mbd -, you get a report of services running that include the string mbd in their names. This includes both the Samba daemons, and normally not much else.

Here's some sample output from my system:

```
8243 ?  S  0:00 smbd -D
8254 ?  S  0:00 nmbd -D
```
