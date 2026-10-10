
## Table 13-8: Examples of pax Use

| The pax Command | Description |
| :-- | :-- |
| pax -f myfiles | List the contents of the archive named myfiles. |
| pax -r -f myfiles | Extract the contents of the archive named myfiles. |
| pax -w -f myfiles /etc | Create an archive named myfiles containing everything within the /etc directory. |
| pax -w -f myfiles *.txt | Archive all of the files in the current directory that have a .txt file extension. |
| pax -r -w /olddir /newdir | Copy the entire contents of the directory /olddir into a new directory called /newdir. |
| pax -w -B 1440000 -F /dev/fd0 * | Archive the contents of the current directory onto multiple floppy disks. |
| pax -w -x cpio -f myfiles * | Archive the contents of the current directory into an archive file named myfiles using the cpio format. |
| pax -r -U mary -f backups | Extract all of the files owned by user mary from the archive named backups. |

Note that by leaving off both the -r and -w options, you cause pax to simply list the contents of the archive. If you specify both the -r and -w options, then you should leave off the -f option and supply source and destination directories instead. This will cause the source directory to be completely cloned in the specified destination directory.

You can use additional parameters to further modify the pax command's behavior. For example, you can use the -x option in conjunction with the -w option to specify the specific archive type to create, or you can use the -B option to specify the number of bytes to write to each volume of a multivolume archive.

Table 13-9 describes the many optional parameters to the pax command.

## Table 13-9: Options to pax

| Options to pax | Description |
| :-- | :-- |
| -r | Read files from an archive. |
| -w | Write files to an archive. |
| -a | Append files to a previously created archive. |
| -b blocksize | Specify the archive's data block size. It must be a multiple of 512. |
| -c pattern | Match all files except those that match the specified pattern. |
| -d | Match filename wildcards against file or directory names only, not the complete path. |
| -f archive | Specify the name of the archive. |
| -i | Interactively rename files when archiving. |
| -k | Do not overwrite existing files. |
| -l | Link files with hard links when in copy mode (-r -w). |
| -n pattern | Match only the first file that matches the supplied pattern. |
| -o options | Extra options specific to the archiving format used. |
| -p string | Specify the file characteristics to retain when archiving or copying. Read the pax man page for more information on this option. |
| -s repltstr | Modify the archived filenames using the supplied regular expression. |
| -t | Preserve the access times of archived files. |
| -u | Do not overwrite files with older versions. |
| -v | Provide verbose output when running. |
| -x format | Specify the format of the archive. Valid formats include cpio, bcpio, sv4cpio, sv4crc, tar, and ustar. The default is to use ustar when creating an archive. The pax command will automatically determine the correct file type when reading an archive. |
| -z | Indicates that gzip should be used to compress and decompress the archive. |
| -B bytes | Specify the number of bytes per archive volume. Use this option to create multivolume archives on removable media. |
| -D | Do not overwrite existing files with files that have an older inode modification time. |
| -E limit | Limit the number of times pax will retry on encountering a read or write error. |
| -G group | Select files based on a group name or GID. To select by GID, place a # sign in front of the group number. |
| -H | Follow only command-line symbolic links while performing a physical file system traversal. |
| -L | Follow all symbolic links when traversing a directory hierarchy. |
| -P | Do not follow symbolic links. This is the default. |
| -T time | Select files based on their modification time. Read the pax man page for complete discussion of this parameter's syntax. |
| -U user | Select files based on the owner’s user name, or by UID with a # sign in front of it. |
| -X | Do not traverse into directories that reside on a different device. |
| -Y | This option is the same as the `-D` option, *except* that the inode change time is checked using the pathname created after all the filename modifications have completed. |
| -Z | This option is the same as the `-u` option, *except* that the modification time is checked using the pathname created after all the filename modifications have completed. |

As you can see, pax is a very flexible and powerful archiving tool. It can be particularly helpful in migrating data from older legacy systems to your new Linux system. When you are faced with the task of recovering archived data from an antiquated or even nonfunctioning UNIX system, the multiple file format support of pax can be a literal lifesaver.

## Summary

I hope that you never experience a major hard drive crash, but if you do, the effort of making backups will repay itself many times over. A variety of low-cost backup hardware is available to use with your Fedora or RHEL system. The traditional tape drive is an excellent choice for backing up large amounts of data or data that you need to keep for years. However, simply copying your /home directories to another medium offers some level of protection for your data.

For convenience, a writable DVD or CD drive is a good choice. As for the tools you choose to do your backups, the dump and restore commands are old favorites, dating back to the early UNIX days (although they are considered somewhat unreliable these days). The Amanda backup facility is excellent for network backups. If you are dealing with backups in several different formats, the pax command might be helpful.

# Chapter 14

## Computer Security Issues

**In This Chapter**

-   * Linux security checklist
-   * Using password protection
-   * Protecting Linux with iptables firewalls
-   * Service access control with TCP wrappers
-   * Checking log files
-   * Using secure shell package
-   * Understanding attack techniques
-   * Securing servers with SELinux
-   * Protecting servers with encryption and certificates

With the growth of the Internet, computer and network security has become more important than ever. Assaults on your Fedora or Red Hat Enterprise Linux system can come in many forms, such as denial-of-service attacks, break-in attempts, or hijacking your machine as a spam relay, to name a few.

In many cases, good practices for setting and protecting passwords, monitoring log files, and creating good firewalls will keep out many would-be intruders. Keeping up with critical security software updates will help patch vulnerabilities as they become known. The recent addition of SELinux adds another layer of protection on your Linux system. Sometimes, more proactive approaches are needed to respond to break-ins. This chapter will familiarize you, as a Linux administrator, with the dangers that exist and the tools necessary to protect your system.

## Linux Security Checklist

While Linux offers all the tools you need to secure your computer, if you are careless, someone can (and probably will) harm your system or try to steal your data. The following checklist covers a range of security measures to protect your Linux desktop or server.

-   **Add users and passwords** — Creating separate user accounts (each with a good password) is your first line of defense in keeping your data secure. Users are protected from each other, as well as from an outsider who takes over one user account. Setting up group accounts can extend the concept of ownership to multiple users. See Chapter 11 for more on setting up user accounts and “Using Password Protection” later in this chapter.
-   **Read, write, and execute permissions** — Every item in a Linux file system (including files, directories, applications, and devices) can be restricted by read, write, and execute permissions for that item’s owner and group, as well as by all others. In this way, for example, you can let other users run a command or open a file, allowing them to change it. See Chapter 4 for information on setting file and directory permissions.
-   **Protect root** — In standard Linux systems, the root users (as well as other administrative user accounts such as apache) have special abilities to use and change your Linux system. Protect the root account’s password and don’t use the root account when you don’t need to. An open shell or desktop owned by the root user can be a target for attack. Running `system-config-*` windows as a regular user (and then entering the root password as prompted) and running administrative commands using `sudo` can reduce exposure to attacks on your root account. See Chapter 10 for information on handling the root user account.
-   **Use trusted software** — While there are no guarantees with any open source software, you have a better chance of avoiding compromised software by using an established Linux distribution (such as Fedora or RHEL). Software repositories where you get add-on packages or updates should likewise be scrutinized. Using valid GPG public keys (which use signatures and encryption) you can ensure that the software you install comes from a valid vendor. And, of course, always be sure of the source of data files you receive before opening them in a Linux application.
-   **Get software updates** — As vulnerabilities and bugs are discovered in software packages, every major Linux distribution (including RHEL and Fedora) offers tools for getting and installing those updates. Be sure to get those updates, especially if you are using Linux as a server. See Chapter 5 for information on using Package Manager, Package Updater, and yum to get software updates.
-   **Use secure applications** — Even with software that is valid and working, some applications offer better protection from attack or invasion than others. For example, if you want to log in to a computer over the Internet, the secure shell service (ssh) is considered more secure than `rlogin` or `telnet` services. Also, some services that are thought to be insecure if you expose them on the Internet (such as Samba and NFS), can be used more securely over the Internet through virtual private network (VPN) tunnels (such as IPSec or CIPE).
-   **Use restrictive firewalls** — A primary job of a firewall is to accept requests for services from a network that you want to allow and turn away requests that you don’t (based on port numbers requested). A desktop system should refuse requests that come in on most ports. A server system should allow requests for a controlled set of ports. This chapter describes how to set up a firewall using iptables.
