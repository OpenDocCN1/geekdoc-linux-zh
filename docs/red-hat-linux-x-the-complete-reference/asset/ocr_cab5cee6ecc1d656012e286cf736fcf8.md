```
pager:
$ ncftp -c ftp.redhat.com/pub/README > ~/redhatinfo/readme
$ ncftp -m ftp.redhat.com/pub/README
```

# NcFTP Download Features

The NcFTP get command differs significantly from the original FTP client's get command. Whereas the original FTP client uses two commands, get and mget, to perform download operations, NcFTP uses only the get command. However, the NcFTP get command combines the capabilities of both mget and get into the get command, as well as adding several new features. Table 14-7 lists the various get command options. By default, the NcFTP get command performs wildcard matching for filenames. If you enter only part of a filename, the get command tries to download all files beginning with that name. You can turn off wildcard matching with the -G option, in which case you must enter the full names of the files you want. The following example downloads all files with names beginning with "Xfree86" and is similar to using mget Xfree86* in the original FTP:

Table 14-7: NcFTP get Options

| Command | Description |
|---|---|
| -G | Turns wildcard matching for filenames on or off |
| -R directory | Downloads a directory and all its subdirectories (recursive) |
| -f filenames | Forces the download of all specified files, even if older or the same as local ones |
| -c | Forces resumption of a download from where it was interrupted |
| -z remote-file local-file | Renames a remote file on your local system |
| -n num | Downloads files no older than the specified number of days |

```
get Xfree86
```

The get command checks to see if you already have a file you are trying to download. If so, it skips the download. The get command also checks if the file you already have is a newer version, in which case it also skips the download. This is a helpful feature for easily maintaining upgrade files. You can simply access the update directory on the remote site, and then use the get command with the * to download to the directory you are using to keep your upgrade file. Only newer versions or newly added upgrade files are downloaded, instead of the entire set. If you want to download a file, even though you have it already, you can force the download with the -f option. For example, to download upgrades for Red Hat manually, you can connect to the Red Hat upgrade directory in the Red Hat FTP site and then issue the following get command:

```
get *
```