
| amandaidx | 10082/tcp |
| amandxtape | 10083/tcp |

## On the amanda server

To offer these services to the network in Fedora, you need to configure the `xinetd` daemon to listen for those services. You do this by enabling the `amandaidx` and `amandx` services by typing the following (as root user):

```
# chkconfig amandx on
# chkconfig amandaidx on
```

This enables Amanda to accept requests from the client system and to start the backup process without any user intervention. You need to tell the `xinetd` daemon to reload the `/etc/xinetd.d` files before this change takes effect. You can do this by typing the following as root user:

```
# /etc/init.d/xinetd reload
```

## On each amanda client

Next you need to configure the `.amandahosts` file in the `/var/lib/amanda` directory on each computer (client) that the amanda server will back up from. This file should contain the fully qualified host and domain name of any backup servers that will connect to this client. When you begin, only your localhost is defined in this file as your backup server. To add another computer as a backup server, type the following (replacing *amandahost* with the name of the backup server, while you are logged in as the amanda user):

```
$ echo amandahost >> /var/lib/amanda/.amandahosts
```

You also need to make sure that the amanda client daemon is configured to run on the client. You do this by enabling the amanda service by typing the following (as root user):

```
# chkconfig amanda on
```

This enables the amanda client to communicate with the amanda server. You need to tell the `xinetd` daemon to reload the `/etc/xinetd.d` files before this change takes place. Do this by typing the following as root user:

```
# /etc/init.d/xinetd reload
```

## Performing an Amanda backup

Now that everything is configured, you are ready to perform an Amanda backup. While logged in as root, type the following command:

```
# /usr/sbin/amdump normal
```

This runs the `amdump` command and tells it to read the configuration files it finds in the `/etc/amanda/normal` directory created earlier. It then works its way down the list of systems and partitions in the `disklist` file, backing up each partition in the order it occurs. The results of the `amdump` are written to the `/var/lib/amanda/normal` directory. Read the files you find there to check on the results of the backup. (See the previous section on how to create a *disklist* file to understand the process that amdump goes through.)

You can, of course, automate this process with *cron*. To create an amdump schedule similar to the regular dump schedule discussed in an earlier section, do the following. While logged in as root, enter the *crontab* command with the -e option:

```
# crontab -e
```

This opens the root crontab file in an editor. Add the following lines to the end of the file:

```
0 22 * * 0 /usr/sbin/amdump normal
0 22 * * 1 /usr/sbin/amdump incremental
0 22 * * 2 /usr/sbin/amdump incremental
0 22 * * 3 /usr/sbin/amdump incremental
0 22 * * 4 /usr/sbin/amdump incremental
0 22 * * 5 /usr/sbin/amdump incremental
0 22 * * 6 /usr/sbin/amdump incremental
```

Save and exit the file. The *cron* daemon will now run *amdump* at 10:00 p.m. (22:00 in military time) every day of the week. This example assumes that a second incremental configuration has been created. You can do this by creating a subdirectory named *incremental* under */etc/amanda* and populating it with appropriately modified *amanda.conf* and *disklist* files. You must also create a subdirectory named *incremental* under */var/lib/amanda* so that amanda has somewhere to write the logfiles for this configuration.

It may be a bit of work to get it all in place, but when you do, Amanda can make your network backups much easier to manage. It may be overkill for a small office, but in a large enterprise network situation, it enables Fedora Core to act as a powerful backup server.

## Using the pax Archiving Tool

Over the years, a variety of UNIX operating systems have arisen, resulting in a variety of similar but incompatible file archiving formats. Even tools that go by the same name may use slightly different storage formats on different systems. This can lead to big problems when trying to archive and retrieve data in a multiplatform environment. Fortunately, there is a solution.

The *pax* program is a POSIX standard utility that can read and write a wide variety of archive formats. An RPM package for *pax* is included with Fedora Core. If it is not already installed, copy the *pax*-* RPM file from your distribution media (CD#1), or download it from a Fedora download site, and then use the *rpm* command to install it.

```
# rpm -Uhv pax-*
```

Remember you need to be logged in as *root* when installing software with the *rpm* command. *Pax* takes a variety of command-line options. The last parameter is usually the file or directory to archive. You may use wildcard characters such as * or ? to specify multiple files or directories. The options you will use most often include the -r and -w parameters for specifying when you are reading or writing an archive. These are usually used in conjunction with the -f parameter, which is used to specify the name of the archive file. By using pax parameters in different combinations, it is possible to extract an archive, create an archive, list the contents of an archive, or even copy an entire directory hierarchy from one location to another. Table 13-8 shows a few examples of the pax command in action.

### Table 13-8: Examples of pax Use

| Pax Command | Description |
|---|---|
| pax -f myfiles | List the contents of the archive named myfiles. |
| pax -r -f myfiles | Extract the contents of the archive named myfiles. |
| pax -w -f myfiles /etc | Create an archive named myfiles containing everything within the /etc directory. |
| pax -w -f myfiles *.txt | Archive all of the files in the current directory that have a .txt file extension. |
| pax -r -w /olddir /newdir | Copy the entire contents of the directory /olddir into a new directory called /newdir. |
| pax -w -B 1440000 -f /dev/fdo * | Archive the contents of the current directory onto multiple floppy disks. |
| pax -w -x cpio -f myfiles * | Archive the contents of the current directory into an archive file named myfiles using the cpio format. |
| pax -r -U mary -f backups | Extract all of the files owned by user mary from the archive named backups. |

Note that by leaving off both the -r and -w options, you cause pax to simply list the contents of the archive. If you specify both the -r and -w options, then you should leave off the -f option and supply source and destination directories instead. This will cause the source directory to be completely cloned in the specified destination directory.

You can use additional parameters to further modify the pax command's behavior. For example, you can use the -x option in conjunction with the -w option to specify the specific archive type to create, or you can use the -B option to specify the number of bytes to write to each volume of a multivolume archive.

Table 13-9 describes the many optional parameters to the pax command.

### Table 13-9: Options for the pax Command

| Pax Options | Description |
|---|---|
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
| -s replstr | Modify the archived filenames using the supplied regular expression. |
| -t | Preserve the access times of archived files. |
| -u | Do not overwrite files with older versions. |
| -v | Provide verbose output when running. |
| -x format | Specify the format of the archive. Valid formats include cpio, bcpio, sv4cpio, sv4crc, tar, and ustar. The default is to use ustar when creating an archive. Pax will automatically determine the correct file type when reading an archive. |
| -z | Indicates that gzip should be used to compress and decompress the archive. |
| -B bytes | Specify the number of bytes per archive volume. Use this option to create multivolume archives on removable media. |
| -D | Do not overwrite existing files with files that have an older inode modification time. |
| -E limit | Limit the number of times pax will retry on encountering a read or write error. |
