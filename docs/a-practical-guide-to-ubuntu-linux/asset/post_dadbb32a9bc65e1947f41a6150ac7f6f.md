
restrict filenames to fewer characters. While you can use any character in a filename, you will avoid confusion if you choose characters from the following list:

- Uppercase letters (A–Z)
- Lowercase letters (a–z)
- Numbers (0–9)
- Underscore (_)
- Period (.)
- Comma (,)

Like the children of one parent, no two files in the same directory can have the same name. (Parents give their children different names because it makes good sense, but Linux requires it.) Files in different directories, like the children of different parents, can have the same name.

The filenames you choose should mean something. Too often a directory is filled with important but unhelpful names as as hold1, wombat, and junk, not to mention foo and foobar. Such names are poor choices because they do not help you recall what you stored in a file. The following filenames conform to the suggested syntax and convey information about the contents of the file:

- correspond
- january
- davis
- reports
- 2001
- acct_payable

When you share your files with users on other systems, you may need to make long filenames differ within the first few characters. Systems running DOS or older versions of Windows have an 8-character filename body limit and a 3-character filename extension length limit. Some UNIX systems have a 14-character limit and older Macintosh systems have a 31-character limit. If you keep the filenames short, they are easy to select; later you can add extensions without exceeding the shorter limits imposed by some filesystems. The disadvantage of short filenames is that they are typically less descriptive than long filenames. Long filenames enable you to assign descriptive names to files. To help you select among files without typing entire filenames, shells support filename completion. For more information about this feature, see the “Filename completion” tip on page 163. 

## FILENAME EXTENSIONS

You can use uppercase and lowercase letters within filenames. Linux is case sensitive, so files named JANUARY, January, and january represent distinct files.

## Do not use SPACES within filenames

Although you can use SPACES within filenames, it is a poor idea. Because a SPACE is a special character, you must quote it on the command line. Quoting a character on the command line can be difficult for a novice and cumbersome for an experienced user. Use periods or underscores instead of SPACES: if you are working with a filename that includes a SPACE, you must quote it on the command line by preceding it with a backslash or by placing quotation marks on either side of the filename. The following commands send the file to the printer:

```
$ ls
$ "my file"
```

A filename extension is the part of the filename following the extended period. The filenames listed in Table 6-1 help the C programming language compiler default to specific extensions; in most cases, filename extensions are optional. Extensions make filenames easy to understand. If you like, you can use periods within the same filename—for example, `notes.txt` or `files.tar.gz`.

**Table 6-1 Filename extensions**

| Filename extension | Meaning of extension |
| :--- | :--- |
| compute.c | A C programming source file |
| compute.o | The object file for compute.c |
| compute | The executable file for compute.c |
| memo.txt | A text file |
| memo.pdf | A PDF file; view with xpdf under a GUI |
| memo.ps | A PostScript file; view with gs under a GUI |
| memo.Z | A file compressed with compress (page 176); use uncompress or gunzip (page 175) to decompress |
| memo.tgz or memo.tar.gz | A tar (page 176) archive of files compressed with gzip (page 175) |
| memo.gz | A file compressed with gzip (page 175); view with zcat and decompress with gunzip (both page 175) |
| memo.bz2 | A file compressed with bzip2 (page 174); view with bzcat and decompress with bzip2 (both page 175) |
| memo.html | A file meant to be viewed as a Web browser, such as Firefox |
| photo.gif, photo.jpg, photo.jpeg, photo.bmp, photo.tif, or photo.tiff | A file containing graphical information, such as a picture |

CHAPTER6 THE LINUX FILESYSTEM

```
login: max
Password:
Last login: Wed Oct 20 11:14 from bravo
$ pwd
/home/max
```

**Figure 6-4 Logging in and displaying the pathname of your home directory

## HIDDEN FILENAMES

A filename that begins with a period is called a *hidden filename* (or a hidden file or an *invisible file*) because ls does not display it. The command -a displays all filenames, even hidden ones. Names of startup files usually begin with a period so that they are hidden and do not clutter a directory listing. The .plan file (page 182) is also hidden. Two special entries—a single and double period (. ..)—appear in every directory (page 210).

## THE WORKING DIRECTORY

While you are logged in a character-based interface to a Linux system, you are always associated with a directory. The directory you are associated with is called the working directory or current directory. Sometimes this association is referred to in a physical sense: "You are in (or working in) the *zach directory.*" The pwd (print working directory) builtin displays the pathname of your working directory.

## YOUR HOME DIRECTORY

When you log in on a Linux system or start a terminal emulator window, the working directory is your home directory. To display the pathname of your home directory, use pwd after you log in (Figure 6-4).

When used without any arguments, the ls displays a list of files in the working directory. Because your home directory has been the only working directory you have used so far, ls has displayed a list of files in your home directory. (All the files you have created up to this point were created in your home directory).

## STARTUP FILES

*Startup files*, which appear in your home directory, give the shell and other programs information about you and your preferences. Frequently one of these files tells you what kind of terminal you are using (page 1106) and enables the sts (set terminal) utility to establish the erase (page 151) and kill line (page 151) keys.

Either you or the system administrator can create a startup file containing commands in your home directory. The shell executes the commands in this file each time you log in. Because the startup files have hidden filenames, you must use the ls -a to see if one is in your home directory. A GUI has many startup files. Usually you do not need to work with these directly but control startup sequences using icons on the desktop. See page 293 for more information about startup files.

![](img/45ff4cd21497435daa35084a84b5d07_255_0.png)
