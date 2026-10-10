
# Table 3.8 (Implied from context "Listing 3.8" earlier, but text says "Note that the first time the cp command is used in Listing 3.8")

Let's clean up the structure. The first page starts with code blocks.

```bash
$ cp Emphasis Story-Line
cp: omitting directory 'Emphasis'
$
$ ls -F
Emphasis/
$
$ cp -R Emphasis Story-Line
$
$ ls -F
Emphasis/  Story-Line/
$
$ ls -R Emphasis
Emphasis:
chivalric-romance.txt      melodrama.txt
interplanetary-battles.txt space-warfare.txt
$
$ ls -R Story-Line/
Story-Line/:
chivalric-romance.txt      melodrama.txt
interplanetary-battles.txt space-warfare.txt
$
```

Note that the first time the `cp` command is used in Listing 3.8, the `-R` option is not used, and thus the source directory is not copied. The error message generated, `cp: omitting directory`, can be a little confusing, but essentially it is telling you that the copy will not take place. When the `cp -R` command is used to copy the source directory in Listing 3.8, it is successful. The recursive copy option is one of the few command options that can be uppercase, `-R`, or lowercase, `-r`.

To move or rename a file or directory locally, you use a single command: `mv`. The command's basic syntax is nearly the same as the `cp` command:

```bash
mv [OPTION]... SOURCE DEST
```

The commonly used `mv` command options are similar to `cp` command options. However, you'll notice in Table 3.3 that there are fewer typical `mv` command options than common `cp` options. As always, be sure to view the `mv` utility's man pages, using the `man mv` command, to review all the options for certification studying purposes and explore uncommon options, which may be useful to you.

The move command is simple to use. A few examples of renaming a file as well as employing the `-i` option to avoid renaming a file to a preexisting file are shown in Listing 3.9.

## TABLE 3.3 The mv command's commonly used options

| Short | Long | Description |
| :--- | :--- | :--- |
| `-f` | `--force` | Overwrite any preexisting destination files with the same name as `DEST` |
| `-i` | `--interactive` | Ask before overwriting any preexisting destination files with the same name as `DEST` |
| `-n` | `--no-clobber` | Do not overwrite any preexisting destination files with the same name as `DEST` |
| `-u` | `--update` | Only overwrite preexisting destination files with the same name as `DEST` if the source file is newer |
| `-v` | `--verbose` | Provide detailed command action information as the command executes |

### Listing 3.9: Using the `mv` command

```bash
$ ls
chivalric-romance.txt    melodrama.txt
interplanetary-battles.txt  space-warfare.txt
$
$ mv space-warfare.txt risk-taking.txt
$
$ ls
chivalric-romance.txt    melodrama.txt
interplanetary-battles.txt  risk-taking.txt
$
$ mv -i risk-taking.txt melodrama.txt
mv: overwrite 'melodrama.txt'? n
$
```

When renaming an entire directory, there are no additional required command options. Just issue the `mv` command as you would for renaming a file, as shown in Listing 3.10.

### Listing 3.10: Renaming a directory using the `mv` command

```bash
$ pwd
/home/Christine/SpaceOpera
$
$ ls -F
Emphasis/  Story-Line/
$
$ mv -i Story-Line Story-Topics
$
$ ls -F
Emphasis/  Story-Topics/
$
$ pwd
/home/Christine/SpaceOpera
$
$ ls
Emphasis  Story-Topics
$
$ ls Emphasis/
chivalric-romance.txt          melodrama.txt
interplanetary-battles.txt     risk-taking.txt
$
$ ls Story-Topics/
chivalric-romance.txt          melodrama.txt
interplanetary-battles.txt     space-warfare.txt
$
$ mv Emphasis/risk-taking.txt Story-Topics/risks.txt
$
$ ls Emphasis/
chivalric-romance.txt  interplanetary-battles.txt  melodrama.txt
$
$ ls Story-Topics/
chivalric-romance.txt          melodrama.txt  space-warfare.txt
interplanetary-battles.txt     risks.txt
$
```

You can move a file and rename it all in one simple **mv** command, as shown in Listing 3.11. The *SOURCE* uses the file’s current directory reference and current name. The *DEST* uses the file’s new location as well as its new name.

### Listing 3.11: Moving and renaming a file using the **mv** command

In Listing 3.11, the file *risk-taking.txt* is located in the *Emphasis* directory. Employing a single **mv** command, it is moved to the *Story-Topics* directory and renamed to *risks.txt* at the same time.

For lightning-fast copies of big files or when you are copying large groups of files, the remote sync utility is rather useful. This tool is often used to create backups, can securely copy files over a network, and is accessed via the **rsync** command.

![](img/c0a399aca0d18f8822d714ad0a173123_120_0.png)

> When you're copying files over a network to a remote host, the file transfer process typically needs protection via encryption methods. The `rsync` command can be tunneled through OpenSSH to provide data privacy. Also, the `scp` command can be employed to provide a secure file copy mechanism. Both of these methods are covered in Chapter 12, "Protecting Files."

To quickly copy a file locally, the `rsync` command syntax is similar to the `mv` command's syntax. It is as follows:

```bash
rsync [OPTION] ... SOURCE DEST
```

Certain `rsync` options will assist you in making quick file copies. Certain switches are helpful for copying large files or creating backups locally, so it's a good idea to review the commonly used `rsync` options listed in Table 3.4.

## TABLE 3.4 The `rsync` command's commonly used local copy options

| Short | Long | Description |
| :--- | :--- | :--- |
| `-a` | `--archive` | Use archive mode. |
| `-D` | N/A | Retain device and special files. |
| `-g` | `--group` | Retain file's group. |
| `-h` | `--human-readable` | Display any numeric output in a human-readable format. |
| `-l` | `--links` | Copy symbolic links as symbolic links. |
| `-o` | `--owner` | Retain file's owner. |
| `-p` | `--perms` | Retain file's permissions. |
| N/A | `--progress` | Display progression of file copy process. |
| `-r` | `--recursive` | Copy a directory's contents, and for any subdirectory within the original directory tree, consecutively copy its contents as well (recursive). |
| N/A | `--stats` | Display detailed file transfer statistics. |
| `-t` | `--times` | Retain file's modification time. |
| `-v` | `--verbose` | Provide detailed command action information as command executes. |

Archive mode, turned on by the `-a` (or `--archive`) switch, is an interesting feature. Using this one switch is equivalent to using the option combination of `-rlptgoD`, which is a popular `rsync` command option set for creating directory tree backups.

An example of using the `rsync` utility to copy a large file is shown in Listing 3.12. Notice that when the copy is complete, the utility outputs useful information, such as the data transfer rate. If you want additional file transfer statistics, add the `--stats` option to your command.

### Listing 3.12: Moving and renaming a file using the rsync command

```bash
# ls -sh /media/USB/Parrot-full-3.7_amd64.iso
3.6G /media/USB/Parrot-full-3.7_amd64.iso
#
# rsync -v /media/USB/Parrot-full-3.7_amd64.iso /home/Christine/
Parrot-full-3.7_amd64.iso

sent 3,769,141,763 bytes  received 35 bytes  3,137,030.20 bytes/sec
total size is 3,768,221,696  speedup is 1.00

# ls -sh /home/Christine/Parrot-full-3.7_amd64.iso
3.6G /home/Christine/Parrot-full-3.7_amd64.iso
#
```

![](img/c0a399aca0d18f8822d714ad0a173123_121_0.png)

The remote sync utility will often display a speedup rating in its output. This rating is related to conducting synchronized backups. If you are using the `rsync` command to conduct periodic backups of a particular directory to another directory location, the speedup rating lets you know how many files did not need to be copied because they had not been modified and were already backed up. For example, if 600 of 600 files had to be copied to the backup directory location, the speedup is 1.00. If only 300 of 600 files had to be copied, the speedup is 2.00. Thus, whenever you are using the `rsync` command to copy a single file to a new location, the speedup will always be 1.00.

## Removing Files

Tidying up an entire filesystem or simply your own directory space often starts by deleting unneeded files and directories. Understanding the commands and their switches to do so is paramount to avoid mistakes in removing these items.

The most flexible and heavily used deletion utility is the remove tool. It is employed via the `rm` command, and the basic syntax is:

```bash
rm [OPTION]... FILE
```
