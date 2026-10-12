
## Using the Amanda Backup Application

Provided with Fedora, Amanda is a powerful, network backup application created by the University of Maryland at College Park. Amanda is a robust backup and restore application best suited for unattended backups with an autoloading tape drive of adequate capacity. It benefits from good user support and documentation.

Amanda's features include compression and encryption. It is intended for use with high-capacity tape drives, floppietal, CD-R, and CD-RW devices.

Amanda uses GNU tar and dump. It is intended for unattended, automated tape backups, and is not well-suited for interactive or ad hoc backups. The support for tape devices in Amanda is robust, and file restoration is relatively simple. Although Amanda does not support older Macintosh clients, it will use Samba to back up Microsoft Windows clients, as well as any UNIX client that can use GNU tools (which includes Mac OS X). Because Amanda runs on top of standard GNU tools, file restoration can be made using those tools on a recovery disk even if the Amanda server is not available. File compression can be done on either the client or server, thus lightening the computational load on less powerful machines that need backing up.

> **CAUTION**
>
> Amanda does not support dump images larger than a single tape and requires a new tape for each run. If you forget to change a tape, Amanda continues to attempt backups until you insert a new tape, but those backups will not capture the data as you intended them to. Do not use too small a tape or forget to change a tape, or you will not be happy with the results.

There is no GUI interface for Amanda. Configuration is done in the time-honored UNIX tradition of editing text configuration files located in `/etc/amanda`. The default installation in Fedora includes a sample cron file because it is expected that you will be using cron to run Amanda regularly. The client utilities are installed with the package `am-utils`; the Amanda server must be obtained from the Amanda website. As far as backup schemes are concerned, Amanda calculates an optimal scheme on-the-fly and schedules it accordingly. It can be forced to adhere to a traditional scheme, but other tools are possibly better suited for that job.

The man page for Amanda (the client is `amdump`) is well written and useful, explaining the configuration of Amanda as well as detailing the programs that actually make up Amanda. The configuration files found in `/etc/amanda` are well commented; they provide a number of examples to assist you in configuration.

The program's home page is http://www.amanda.org/. There, you will find information on subscribing to the mail list, as well as links to Amanda-related projects and a FAQ.

## Alternative Backup Software

The free download version of Fedora does not provide any other sophisticated backup applications, but the version targeted to businesses usually does. Commercial and other freeware backup products do exist; BRU and Veritas are good examples of effective commercial backup products. Here are some useful free software backup tools that are not installed with Fedora:

- `flexbackup` — This backup tool is a large file of Perl scripts that makes dump and restore easier to use. flexbackup's command syntax can be accessed by using the command with the -help argument. It also can use afio, cpio, and tar to create and restore archives locally or over a network using rsh or ssh if security is a concern. Its home page is http://www.flexbackup.org/.
- `afio` — This tool creates cpio-formatted archives, but handles input data corruption better than cpio (which does not handle data input corruption very well at all). It supports multivolume archives during interactive operation and can make compressed archives. If you feel the need to use cpio, you might want to check out afio at http://freshmeat.net/projects/afio/.
- `cdbackup` — Designed for the home or small office user, cdbackup works with any backup and restores software that can read from stdin, write to stdout, and can handle linear devices such as tape drives. It makes it easier to use CD-Rs as the storage medium. Similar applications are available elsewhere as well; the home page for this application is at http://www.muempf.de/index.html.

Many other alternative backup tools exist, but covering all of them is beyond the scope of this book. Two good places to look for free backup software are Freshmeat (http://www.freshmeat.net/) and Google (http://www.google.com/linux).

## Copying Files

Often, when you have only a few files that you need to protect from loss or corruption, it might make better sense to simply copy the individual files to another storage medium rather than to create an archive of them. You can use the tar, cp, rsync, or even the cpio commands to do this, as well as a handy file management tool known as mc. Using tar is the traditional choice because older versions of cp did not handle symbolic links and permissions well at times, causing those attributes (characteristics of the file) to be lost; tar handled those file attributes in a better manner. cp has been improved to fix those problems, but tar is still more widely used. rsync has recently been added to Fedora and is an excellent choice for mirroring sets of files, especially when done over a network.

To illustrate how to use file copying as a backup technique, the examples here show how to copy (not archive) a directory tree. This tree includes symbolic links and files that have special file permissions we need to keep intact.

### Copying Files Using tar

One choice for copying files into another location is to use the tar command where you would create a tar file that would be piped to tar to be uncompressed in the new location. To accomplish this, first change to the source directory. Then, the entire command resembles

```bash
# tar cvf - files | ( cd target_directory ; tar xpf - )
```

where `files` are the filenames you want to include; use `*` to include the entire current directory.

Here is how the command shown works: You have already changed to the source directory and executed tar with the `cvf -` arguments that tell tar to:

- `c` — Create an archive.
- `v` — Verbose; lists the files processed so we can see that it is working.
- `f` — The filename of the archive will be what follows. (In this case, it is `-`)
- `-` — A buffer, a place to hold our data temporarily.

The following `tar` commands can be useful for creating file copies for backup purposes:

1. Stay in the local file system (so that you do not include remote volumes).
   - `tar tvf -` — List but not tar files.
   - `tar xvf -` — Do not care about access times on files, even though you are accessing them now, to preserve the old access information for archival purposes.

The contents of the tar file (held for us temporarily in the buffer, which is named `-`) are then piped to the second expression, which extracts the files to the target directory. In shell programming (refer to Chapter 14, “Managing Users”), enclosing an expression in parentheses causes it to operate in a subshell and be executed first.

First we change to the target directory, and then

- `x` — Extract files from a tar archive.
- `p` — Preserve permissions.
- `f` — The filename will be `-`, the temporary buffer that holds the tarred files.

### Compressing, Encrypting, and Sending tar Streams

The file copy techniques using the tar command in the previous section can also be used to quickly and securely copy a directory structure across a LAN or the Internet (using the `ssh` command). One way to make use of these techniques is to use the following command line to first compress the contents of a designated directory, and then decompress the compressed and encrypted archive stream into a designated directory on a remote host:

```bash
$ tar cvzf - data_folder | ssh remote_host 'cd ~/mybackup_dir ; tar xvzf -'
```

The `tar` command is used to create, list, and compress the files in the directory named `data_folder`. The output is piped through the `ssh` (secure shell) command and sent to the remote computer named `remote_host`. On the remote computer, the stream is then extracted and saved in the directory named `~/mybackup_dir`. You will be prompted for a password in order to send the stream.
