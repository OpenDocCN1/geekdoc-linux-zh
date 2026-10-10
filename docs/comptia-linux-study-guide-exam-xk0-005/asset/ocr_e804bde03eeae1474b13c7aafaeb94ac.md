Another good practice is to verify your backup automatically immediately after the tar archive is created. This is easily accomplished by tacking on the `-W` option, as shown in Listing 12.11.

# Listing 12.11 Using tar to verify backed-up files automatically

```
```console
$ tar -Wcvf ProjectVerify.tar Project4?.txt
Project42.txt
Project43.txt
Project44.txt
Project45.txt
Project46.txt
Verify Project42.txt
Verify Project43.txt
Verify Project44.txt
Verify Project45.txt
Verify Project46.txt
$
```
```

You cannot use the `-W` option if you employ compression to create a tarball. However, you could create and verify the archive first and then compress it in a separate step. You can also use the `-W` option when you extract files from a tar archive. This is handy for instantly verifying files restored from archives.

Table 12.4 lists some of the options that you can use with the tar utility to restore data from a tar archive file or tarball. Be aware that several options used to create the backup, such as `-g` and `-W`, can also be used when restoring data.

TABLE 12.4 The tar command's commonly used file restore options

| Short | Long | Description |
|:---|:---|:---|
| `-x` | `--extract` | Extracts files from a tarball or archive file and places them in the current working directory |
| | `--get` | |
| `-z` | `--gunzip` | Decompresses files in a tarball using gunzip |
| `-j` | `--bunzip2` | Decompresses files in a tarball using bunzip2 |
| `-J` | `--unxz` | Decompresses files in a tarball using unxz |

Extracting files from an archive or tarball is fairly simple using the tar utility. Listing 12.12 shows an example of extracting files from a previously created tarball.