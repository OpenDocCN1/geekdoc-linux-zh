
## When the number of files to be located by find is relatively small

No one really wants to sit at a terminal for a long time typing `y` and `Enter` or `n` and `Enter` repeatedly. This activity is tedious, and tedious activities can lead to mistakes.

Table 8.1 lists some other common options that you can specify with the `find` command. For even more options, consult your information sources.

### Example 8.3 find with an Interactive Action

Sancho is convinced now that his `misc` files should be deleted. He will use `find` in combination with a single action, but he will do it interactively. Doing it interactively is a good thing—he is about to make a typographical error in his command sequence. But the interactivity will enable him to prevent the wrong files from being deleted:

```bash
$ find . -name 'm\*' -ok rm { } \; <Enter>
< rm ... ../mbox > ? n<Enter>
< rm ... ../misc > ? y<Enter>
< rm ... ./Misc/misc > ? y<Enter>
< rm ... ./Admin/memos > ? n<Enter>
< rm ... ./Admin/misc > y<Enter>
< rm ... ./Main/misc > ? y<Enter>
```

### Table 8.1 Selected find Options

| OPTION | DESCRIPTION |
| :--- | :--- |
| -type c | Find files of type c (character special file). The type can also be b (block special file), d (directory), f (plain file), l (symbolic link), p (fifo or a named pipe), or s (socket). |
| -size n[c] | Find files containing n blocks, or if c is specified, n characters long (1 block = 4,096 bytes) |
| -mtime +n \| n \| -n | Find files that were last modified more than (+n), less than (-n), or exactly (n) days ago |
| -perm nnn | Find files whose permissions are set to octal number nnn |
| -user username | Find files belonging to the specified user |
| -o | Find files that match specified conditions |
| -newer filename | Find files that have been modified more recently than filename. (Note the similarity to mtime.) |

If Sancho had not made the command interactive, then his `mbox` and `/admin/memos` files would also have been deleted.

## Using Additional Options with the find Command

This section includes four examples of `find` command options. Most of these options were described in the preceding section.

### Example 8.4 find with a Line Continuation (Split Command)

Sancho remembers working on a profile of each of the two “beasts of burden” (Rozinante and Dapple) recently but has forgotten where he filed them. He knows they are both medium to small documents and that they are in his directory structure somewhere, so he enters:

```bash
$ cd <Enter>
$ pwd <Enter>
/home/panzasasn
$ find . -mtime -1 -type f -size +500c <Enter>
> -exec ls -l { } \; <Enter>
-rw------- panzasasn knights1 682 Jul 02 14:49 mbox
-rw------- panzasasn knights1 3930 Jul 02 08:32 /.bash_history
-rw-r--r-- panzasasn knights1 667 Jul 21 14:49 ./maint/rozinante
-rw-r--r-- panzasasn knights1 993 Jul 22 09:44 ./Main/dapple
-rw-r--r-- panzasasn knights1 642 Jul 22 11:13 /.fles
```

Here, he split the command so that one part is written opposite the primary prompt and the rest is written opposite the secondary prompt. We had Sancho perform this action to show how this command form works (and to show that it will work).

What is the command requesting? It says, “Starting from the current directory, find all files that are larger than 500 characters in length and that were modified within the last day. Then, as each successful file is found, create a long listing of it and present the long listing on the terminal screen.” And, after a quick perusal of the response, Sancho sees that his two files are in his `/home/panzasasn/maint` subdirectory.

### Example 8.5 find with Complex Options

Freston is randomly checking the permissions on files to see whether any staff members have altered their `umask` to `002` for file creation in their home directories during the past calendar week:

```bash
# cd <Enter>
# pwd <Enter>
/
# find ./home -perm 664 -mtime -7 -print <Enter>
./home/perez/Quixote
```

In other words, in Example 8.5, Freston requested that the system find and display—again, from the current directory downward—the names of all files created in the past seven days with permissions set to 664 (that is, `rw-rw-r--`).

Freston makes a note to call Perez and ask him why he has created the `Quixote` file with the permissions it has. Meanwhile, if you have any concerns regarding permission bits, please review the discussion in Chapter 6, “Linux File Permissions.”

### Example 8.6 find with the -o (OR) option

Sancho was working on profiles of both Rozinante and Dapple recently. Now, he has lost track of where he filed them. Luckily, he remembers their names. Here is how he finds them:

```bash
$ cd <Enter>
$ pwd <Enter>
/home/panzasan
$ find . -name rozinante -o -name dapple <Enter>
./Admin/rozinante
./Admin/dapple
```

In other words, Sancho requested that the system find and display the names of all files named `rozinante` or `dapple` from his current directory downward.

### Example 8.7 find with Error Redirection

Freston was explaining to Sancho how he (Freston) was searching the whole directory structure for files pertaining to security that have the word `security` as part of their path name. He told Sancho how he (Freston) would do it:

```bash
# cd /
# find / -name "security" -print 2> errfile <Enter>
/etc/security
/usr/include/security
/lib/security
```

Interpreting his command, we see that Preston, in Example 8.7, requested that the system find, from the root directory downward (that is, through the entire system file structure), filenames containing the `security` text string as part of their path name. Then, the system was to display the successful path names on the terminal screen. Errors are not to be displayed on the screen but instead are to be listed in the `errfile` file in the current directory. If such a file does not exist, the command creates it.

Sancho, after a moment, tells Preston that he did the same thing and got the same result:

```bash
$ cd /
$ find / -name "security" -print 2> errfile <Enter>
/etc/security
/usr/include/security
/lib/security
```

Preston says, “Well, Sancho, although you (fortunately, even luckily) got the same output to the screen that I did, you didn’t really get the same result. When I `cat`’d my `errfile`, I found it to be empty. So I’m confident that I was able to examine all directories. Why? My `errfile` is empty?”

Sancho checks and tells him, “No way! My `errfile` is full of errors! Many directories didn’t allow me entry at all!”

The lesson here is to be careful with commands like this one. If the command does not appear to provide the expected output, or even if it does, it might still have created errors. But you will not know about the errors unless you check the `errfile` file. An ordinary user (as opposed to a superuser or a root user) is likely to encounter more errors in these situations due to a lack of permissions on directories or files.

## Locating Commands: whatis, whereis, and which Commands

What if you are trying to execute a program and the shell tells you it cannot find the file or directory you refer to when you use the name of the command? Or, what if you are writing a program that will invoke a command and you need the full path name of the command, but you do not know where it resides? Here are three quick *find*-like utilities that can help.

### whatis

When you are not sure of a command name, when you are not sure of exactly what the command will do, or even when you want to resolve arguments among colleagues, the `whatis` command can be helpful. The `whatis` command searches the `whatis` database, a file found in the `/usr/bin` directory, for the command name that you want to investigate and then prints a brief summary of what that command does when invoked. The syntax for `whatis` is straightforward:

```bash
$ whatis commandname <Enter>
```

Be sure to use a complete word. No partial text strings are allowed. See Example 8.8.

#### Example 8.8 whatis

Sancho and the others have been advised to use the `grep` command to search for information within their files without having to `cat` them individually. Before he actually uses `grep`, Sancho decides to investigate it. He starts with `whatis` as follows:

```bash
$ whatis grep <Enter>
grep (1) - print lines matching a pattern
```

Thanks to `whatis`, Sancho at least has verified the correct command name to continue his search (if he decides to do so). If he had the wrong name to begin with (such as “`gresp`” or something), he might have had to enter `whatis` several times to nail down the correct name. If more information is required, Sancho can search `grep`’s man pages or other information sources.

### which

The `which` command is different from both `whatis` and `whereis`. It lists the path names of the files that will be executed if you run the specified command. Unlike `whereis` (which we will look at next), `which` searches your `PATH` variable. The major drawback to `which` is that it stops searching after it finds and reports on the first occurrence of the command name.
