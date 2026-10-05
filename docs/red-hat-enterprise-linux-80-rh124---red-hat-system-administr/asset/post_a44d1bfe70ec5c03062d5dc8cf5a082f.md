
```
/usr/lib/sysimage
/usr/lib/dracut/dracut.conf.d/02-generic-image.conf
/usr/lib/firewall/services/ovirt-imageio.xml
/usr/lib/grub/1386-pc/lnxboot.image
...output omitted.
```

The -i option performs a case-insensitive search. With this option, all possible combinations of upper and lowercase letters match the search.

```bash
[user@host ~]$ locate -i messages
...output omitted.
/usr/share/vim80/log/zh_TW_LC_MESSAGES
/usr/share/vim80/log/zh_TW_LC_MESSAGES/vim.mo
/usr/share/vim80/log/zh_TW.UTF-8/LC_MESSAGES
/usr/share/vim80/log/zh_TW.UTF-8/LC_MESSAGES/vim.mo
/usr/share/vim80/syntax/messages.vim
/usr/share/vim80/syntax/msmessages.vim
/var/log/messages
```

The -n option limits the number of returned search results by the locate command. Example limits the search results returned by locate to the first five:

```bash
[user@host ~]$ locate -n 5 snow.png
/usr/share/icons/HighContrast/16x16/status/weather-snow.png
/usr/share/icons/HighContrast/22x22/status/weather-snow.png
/usr/share/icons/HighContrast/24x24/status/weather-snow.png
/usr/share/icons/HighContrast/25x25/status/weather-snow.png
/usr/share/icons/HighContrast/32x32/status/weather-snow.png
```

# SEARCHING FOR FILES IN REAL TIME

The find command locates files by performing a real-time search in the file-system hierarchy. It is slower than locate, but more accurate. It can also search for files based on criteria other than the file name, such as the permissions of file, type of file, its size, or its modification time.

The find command locates files in the file system using the user account that executed the search. The user invoking the find command must read and execute permission on a directory to examine its contents.

The first argument to the find command is the directory to search. If the directory argument is omitted, find starts in the current directory and looks for matches in any subdirectories.

To search for files by file name, use the -name FILENAME. find returns the path to files matching FILENAME exactly. For example, to search for files named ssh_config starting from the root, run the following command:

```bash
[root@host ~]# find / -name sshd_config
/etc/ssh/sshd_config
```

# NOTE
With the find command, the full word options use a single dash and options follow
the path name argument, unlike most other Linux commands.

Wildcards are available to search for a file name and return all results that are a partial match.
Using wildcards, it is important to quote the file name to look for to prevent the terminal from
interpreting the wildcard.

In the following example, search for files ending in the / directory that ends in .txt:

```bash
[root@host ~]# find -name '*.txt'
/etc/pki/nssdb/pkcs11.txt
/etc/brlty/brl-lt-all.txt
/etc/brlty/brl-mb-all.txt
/etc/brlty/brl-md-all.txt
/etc/brlty/brl-mn-all.txt
...output omitted...
```

Search for files in the /etc/ directory that contains the word, pass, anywhere in their names on
host, run the following command:

```bash
[root@host ~]# find /etc -name '*pass*'
/etc/security/opasswd
/etc/pam.d/passwd
/etc/pam.d/password-auth
/etc/passwd
/etc/passwd
/etc/authselect/password-auth
```

To perform a case-insensitive search for a given file name, use the -iname option, followed by the
file name to search. Search with case-insensitive text, messages, in their names in the /
directory on host, run the following command:

```bash
[root@host ~]# find -iname '*messages*'
...output omitted...
/usr/share/vim80/lang_zh.UTF-8/LC_MAGES
/usr/share/vim80/lang_zh.cp936/LC_MAGES
/usr/share/vim80/lang_zh.TW/LC_MAGES
/usr/share/vim80/lang_zh.TW.UTF-8/LC_MAGES
/usr/share/vim80/syntax/messages.vim
/usr/share/vim80/syntax/msmessages.vim
```

# Searching Files Based on Ownership or Permission

The find command can search for files based on ownership or permissions. Useful options
when searching by user are -user and -group, search by name, -uid and -gid.

Search for files owned by user in the /home/user directory on host.

```bash
[user@host ~] find -user user
```

# CHAPTER 12 | Accessing Linux Systems

Search for files owned by user in the /home/user directory on host.

```bash
[user@host ~] find -user user
./bash_logout
./bashprofile
./bashrc
```

Search for files owned by the group in the /home/user directory on host.

```bash
[user@host ~]$ find -group user
./bash_logout
./bashprofile
./bashrc
```

Search for files owned by user ID 1000 in the /home/user directory on host.

```bash
[user@host ~]$ find -uid 1000
./bash_logout
./bashprofile
./bashrc
```

Search for files owned by group ID 1000 in the /home/user directory on host.

```bash
[user@host ~]$ find -gid 1000
./bash_logout
./bashprofile
./bashrc
```

The -user, and -group options can be used together to search files where owner and group are different. The example below lists files that are both owned by root and affiliated with mail.

```bash
[user@host ~]$ find / -user root -group mail
/var/spool/mail
...output omitted...
```

The -perm option is used to look for files with a particular set. Permissions can be described
as octal values, with some combination of 4, 2, and 1 for read, write, and execute. Permissions
preceded by / matches files that have at least one bit. A file with permissions 222 does not match,
but something like 644 does. Neither of the previous examples would match.

To use a more complex example, the following command matches any file for which the user has read, write, and execute permissions, the group have read and write permissions, and others have read-only access:

```bash
[root@host ~]# find /home -perm 764
```

To match files for which the user has at least read and execute permissions, the group has at least write permissions, and others have at least read access:

```bash
[root@host ~]# find /home -perm 324
```

To match files for which the user has read permissions, or the group has at least read permissions, or others have at least write access:

```bash
[root@host ~]# find /home -perm 442
```

To match any file in the /home/user/ directory where others have at least read access on host:

```bash
[user@host ~]$ find / -perm -004
```

Find all files in the /home/user directory where others has write permissions on host.

```bash
[user@host ~]$ find /perm -002
```

# Searching Files Based on Size

The **find** command can look up files that match a size specified with the **-size** option,
followed by a numerical value and the unit. Use the following list as the units with the **-size** option:

- **k**, for kilobyte
- **M**, for megabyte
- **G**, for gigabyte

The example below shows how to search for files with a size of 10 megabytes, rounded up.

```bash
[user@host ~]$ find -size 10M
```

To search the files with a size **more than 10** gigabytes.

```bash
[user@host ~]$ find -size +10G
```

To list all files with a size **less than 10** kilobytes.

```bash
[user@host ~]$ find -size -10k
```

# CHAPTER 12 | Accessing Linux Files

> IMPORTANT
> The -size option unit modifiers round up to single units. For example, the find -size 1M command shows files smaller than 1 MB because it rounds all files up to 1 MB.

# Searching Files Based on Modification Time

The -mmin option, followed by the time in minutes, searches for all files that had their content changed at n minutes ago in the past. The file timestamp is always rounded down. It also supports fractional values when using ranges (+n and -n).

To find all files that had their content changed 120 minutes ago on host, run:

```bash
[root@host ~#] find / -mmin 120
```

The + modifier in front of the amount of minutes looks for all files in the / that have been modified more than n minutes ago. In this example, files that were modified more than 200 minutes ago are listed.

```bash
[root@host ~#] find / -mmin +200
```

The - modifier changes the search to look for all files in the / directory which have been changed less than n minutes ago. In this example, files that were modified less than 150 minutes ago are listed.

```bash
[root@host ~#] find / -mmin -150
```

# Searching Files Based on File Type

The -type option in the find command limits the search scope to a given file type. Use the following list to pass the required flags to limit the scope of search:

- f, for regular file
- d, for directory
- l, for soft link
- b, for block device

Search for all directories in the /etc directory on host.

```bash
[root@host ~#] find /etc -type d
/etc
/etc/tmpfiles.d
/etc/systemd
/etc/systemd/system
/etc/systemd/system/getty.target.wants
...output omitted...
```
