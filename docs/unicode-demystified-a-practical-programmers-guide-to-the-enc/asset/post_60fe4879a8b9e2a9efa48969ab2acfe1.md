
-s Displays the size of each file in 1,024-byte blocks. The size precedes the name. With the -l option this option displays the size in column 1 and shifts each of the other items to the right. You can include the -h option to make the files easier to read.

--format=word By default is files sorted vertically. This option sorts files based on word: across (-x), separated by commas (-m), horizontal (-x), long (-l), single-column (-n).

--sort=word By default is displays files in ASCII order. This option sorts the files based on word: filename extension (-X), none (-U), file size (-S), access time (-u), modification time (-t), except see --time.

--time=word By default the time is the modification time of a file. Set word to atime to display access time (or use the -t option) or ctime to display creation time. The file is listed by word when you use the --sort=time option.

ls long (--format=long or -l options) displays the seven columns shown in Figure 4-12 on page 119. The first column, which contains 11 characters, is divided as described in the following paragraphs. The first character describes the type of file, as shown in Table III-20. Refer to pages 103 and 968 for more information on types of files.

# First Character

| First Character | table III-20 |
|---|---|
| - | Ordinary |
| b | Block device |
| c | Character device |
| d | Directory |
| p | FIFO (named pipe) |
| l | Symbolic link |

The next nine characters of the first column represent all the access permissions associated with the file. These nine characters are divided into three sets of three characters each.

The first three characters represent the owner’s access permissions. If the owner has read access permission to the file, an r appears in the first position. If the owner is not permitted to read the file, a hyphen appears in position. The next two positions represent the owner's write and execute access permissions. A w appears in the second position if the owner is permitted to write to the file, and an x appears in the third position if the owner is permitted to execute the file. An s in the third position indicates that the file has set permission and execute permission. A hyphen indicates that the owner does not have the access permission associated with the character position.

In a similar manner the second and third sets of three characters represent the access permissions of the user's group and other users. An s in the third position of the second set of characters indicates that the file has set permission with execute permission, and an s indicates set without execute permission.

The last character is t if the sticky bit is set with execute permission and T if it is set without execute permission. Refer to chmod on page 1103 for information on changing access permissions.

The second column indicates the number of hard links to the file. Refer to page 123 for more information on links.

The third and fourth columns display the name of the owner of the file and the name of the group the file belongs to.

The fifth column indicates the size of the file in bytes or, if information about a device file is being displayed, the size and minor device numbers. In the case of a directory, the number is the size of the directory, not the size of the files that are entries within the directory. (Use du to display the sum of the sizes of all the files in a directory.) Include the -h option to display the size of the file in kilobytes, megabytes, or gigabytes.

The last two columns display the date and time the file was last modified and the filename, respectively.

# Notes

Refer to page 157 for examples of using ls with ambiguous file references.

With the --color option ls can display filenames of various types of files in different colors. By default, executable files are green, directory files are blue, symbolic links are cyan, archives and compressed files are red, and ordinary text files are black. The manner in which ls colors each of the different file types is specified in the /etc/DIR_COLORS file. If this file does not exist on your system, ls will not color filenames. You can modify /etc/DIR_COLORS to alter the default color/filetype mappings on a systemwide basis. For your personal use, you can copy /etc/DIR_COLORS to ~/.dir_colors file in your home directory and modify ~/.dir_colors. For your login, ~/.dir_colors overrides the systemwide colors established in /etc/DIR_COLORS. Refer to the dir_colors and dircolors man pages for more information.

# Examples

The first command shows the ls utility with the -x option. You see an alphabetical list of the names of the files in the working directory:

```
$ ls -x
bin c calendar
execute letters shell
```

The -F option displays a slash (/) to files that are directories, an asterisk to files that are executable, and at an sign (@) symbolic links:

```
$ ls -Fx
bin/ c/ calendar
execute* letters/ shell@
```

The -l (long) option displays a long list. The files are still in alphabetical order:

```
$ ls -l
total 8
drwxrxr-x 2 jenny pubs 80 May 20 09:17 bin
drwxrxr-x 2 jenny pubs 144 Mar 26 11:59 c
-rw-r--r 1 jenny pubs 104 May 28 11:44 calendar
-rw-r--r 1 jenny pubs 85 May 6 08:27 execute
drwxrxr-x 2 jenny pubs 32 Oct 6 22:56 letters
drwxrxr-x 16 jenny pubs 1296 Jun 6 17:33 shell
```

The -a (all) option lists all files, including invisible ones:

```
$ ls -a
.profile c execute shell
bin calendar shell
```

Combining the -a and -l options displays a long listing of all files, including invisible files, in the working directory. This list is still in alphabetical order:

```
$ ls -al
total 12
drwxrxr-x 2 jenny pubs 480 Jun 6 17:42 .
drwxrwx-- 26 root 816 Jun 6 14:45 ..
-rw-r--r 1 jenny pubs 161 Jun 6 17:15 .profile
drwxrxr-x 2 jenny pubs 80 May 20 09:17 bin
drwxrxr-x 2 jenny pubs 144 Mar 26 11:59 c
-rw-r--r 1 jenny pubs 104 May 28 11:44 calendar
-rw-r--r 1 jenny pubs 85 May 6 08:27 execute
drwxrxr-x 2 jenny pubs 32 Oct 6 22:56 letters
drwxrxr-x 16 jenny pubs 1296 Jun 6 17:33 shell
```

When you add the -r (reverse) option to the command line, ls produces a list in reverse alphabetical order:

```
$ ls -alr
total 12
drwxrxr-x 16 jenny pubs 1296 Jun 6 17:33 shell
drwxrxr-x 2 jenny pubs 32 Oct 6 22:56 letters
```

-rw-rw-r-- 1 jenny pubs 85 May 6 08:27 execute
-rw-r--r 1 jenny pubs 104 May 28 11:44 calendar
drwxrxr-x 2 jenny pubs 144 Mar 26 11:59 c
drwxrxr-x 2 jenny pubs 80 May 20 09:17 bin
-rw-r--r 1 jenny pubs 161 Jun 6 17:15 .profile
drwxrwx-- 26 root 816 Jun 6 14:45 ..
drwxrxr-x 2 jenny pubs 480 Jun 6 17:42 .

Use the -t -l options to list files so that the most recently modified file appears at the top:

```
drwxrxr-x 16 jenny pubs 1296 Jun 6 17:33 shell
-rw-r--r 1 jenny pubs 101 Jun 68 11:r-x 1 jenny pubs 80 May 20 09:27 bin
drwxrxr-x 2 jenny pubs 144 Mar 26 11:59 c
drwxrxr-x 2 jenny pubs 32 Oct 6 22:56 letters
-rw-r--r 1 jenny pubs 85 May 6 08:27 execute
-rw-r--r 1 jenny pubs 104 May 28 11:44 calendar
```

Together, the -r -t options will list files with the ones modified least recently at the top of the list:

```
drwxrxr-x 2 jenny pubs 32 Oct 6 22:56 letters
drwxrxr-x 2 jenny pubs 144 Mar 26 11:59 c
-rw-r--r 1 jenny pubs 85 May 6 08:27 execute
drwxrxr-x 2 jenny pubs 80 May 20 09:17 bin
-rw-r--r 1 jenny pubs 104 May 28 11:44 calendar
drwxrxr-x 16 jenny pubs 1296 Jun 6 17:33 shell
```
The next example shows ls with a directory filename as an argument. The ls utility lists the contents of the directory in alphabetical order:

```
$ ls bin
c    lsdir
```

To display information about the directory itself, use the -d (directory) option. This option lists information only about the directory:

```
$ ls -d bin
drwxrxr-x 2 jenny pubs 80 May 20 09:17 bin
```

You can use the following command from bash to display a list of all the filenames (those starting with a period) in your home directory. This is a convenient way to list all initialization files in your home directory:

```
ls -d ~.*
```
