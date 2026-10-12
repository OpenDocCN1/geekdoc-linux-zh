files. You must also create a subdirectory named `incremental` under `/usr/`.

It may be a bit of work to get it all in place, but once you do, Amanda can make your network backups much easier to manage. It may be overkill for a small office, but in a large enterprise network situation, it enables Red Hat Linux to act as a powerful backup server.

# ## Using the pax Archiving Tool

Over the years, a variety of UNIX operating systems have arisen, resulting in a variety of similar but incompatible file archiving formats. Even tools that go by the same name may use slightly different storage formats on different systems. This can lead to big problems when trying to archive and retrieve data in a multiplatform environment. Fortunately, there is a solution.

The `pax` program is a POSIX standard utility that can read and write a wide variety of archive formats. An RPM package for `pax` is included with Red Hat Linux. If it is not already installed, copy the `pax-`* RPM file from your distribution media (CD #1), or download it from a Red Hat Linux FTP site, and then use the `rpm` command to install it.

```
```bash
# rpm -i pax-*
```
```

Remember you need to be logged in as root when installing software with the `rpm` command.

`Pax` takes a variety of command-line options. The last parameter is usually the file or directory to archive. You may use wildcard characters such as `"*"` or `"?"` to specify multiple files or directories. The options you will use most often include the `-r` and `-w` parameters for specifying when you are reading or writing an archive. These are usually used in conjunction with the `-f` parameter, which is used to specify the name of the archive file.

By using `pax` parameters in different combinations, it is possible to extract an archive, create an archive, list the contents of an archive, or even copy an entire directory hierarchy from one location to another. Table 13-8 shows a few examples of the `pax` command in action.

# Table 13-8: Examples of pax Use

| Pax Command | Description |
|---|---|
| pax -f myfile.s | List the contents of the archive named myfile.s |
| pax -r -f myfile.s | Extract the contents of the archive named myfile.s |
| pax -w -f myfile.s /etc | Create an archive named myfile.s containing everything within the /etc directory. |
| pax -w -f myfile.s *.txt | Archive all of the files in the current directory that have a .txt file extension. |