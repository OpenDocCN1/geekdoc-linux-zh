
restrict you to shorter names. While you can use almost any character in a filename, you will avoid confusion if you choose characters from the following list:

- Uppercase letters (A–Z)
- Lowercase letters (a–z)
- Numbers (0–9)
- Underscore (_)
- Period (.)
- Comma (,)

### / or root

The root directory is always named / (slash) and referred to by this single character. No other file can use this name or have a / in its name. However, in a pathname, which is a string of filenames including directory names, the slash separates filenames (page 193).

Like the children of one parent, no two files in the same directory can have the same name. (Parents give their children different names because it makes good sense, but Linux requires it.) Files in different directories, like the children of different parents, can have the same name.

The filenames you choose should mean something. Too often a directory is filled with important files with such unhelpful names as hold1, wombat, and junk, not to mention foo and foodbar. Such names are poor choices because they do not help you recall what you stored in a file. The following filenames conform to the suggested syntax and convey information about the contents of the file:

- correspond
- january
- davis
- reports
- 2001
- acct_payable

### Filename length

When you share your files with users on other systems, you may need to make long filenames differ within the first few characters. Systems running DOS or older versions of Windows have an 8-character filename body length and a 3-character filename extension length limit. Some UNIX systems have a 14-character limit and older Macintosh systems have a 31-character limit. If you keep the filenames short, they are easy to type; later you can add extensions to them without exceeding the shorter limits imposed by some file systems. The disadvantage of short filenames is that they are typically less descriptive than long filenames. See stat on page 440 for a way to determine the maximum length of a filename on the local system.

Long filenames enable you to assign descriptive names to files. To help you select among files without typing entire filenames, shells support filename completion. For more information about this feature, see the “Filename completion” tip on page 151.

### Case sensitivity

You can use uppercase and/or lowercase letters within filenames. Linux is case sensitive, so files named JANUARY, January, and january represent three distinct files.

#### Do not use SPACES within filenames

**caution** Although you can use SPACES within filenames, it is a poor idea. Because a SPACE is a special character, you must quote it on a command line. Quoting a character on a command line can be difficult for a novice user and cumbersome for an experienced user. Use periods or underscores instead of SPACES: joe.05.04.26, new_stuff.

If you are working with a filename that includes a SPACE, such as a file from another operating system, you must quote the SPACE on the command line by preceding it with a backslash or by placing quotation marks on either side of the filename. The two following commands send the file named my file to the printer.

```
$ lpr my\ file
$ lpr "my file"
```

## FILENAME EXTENSIONS

A filename extension is the part of the filename following an embedded period. In the filenames listed in Table 6-1, filename extensions help describe the contents of the file. Some programs, such as the C programming language compiler, default to specific filename extensions; in most cases, however, filename extensions are optional. Use extensions freely to make filenames easy to understand. If you like, you can use several periods within the same filename—for example, notes.4.10.01 or files.tar.gz.

Table 6-1 Filename extensions

| Filename with extension | Meaning of extension |
| :--- | :--- |
| compute.c | A C programming language source file |
| compute.o | The object code for the program |
| compute | The same program as an executable file |
| memo.0410.txt | A text file |
| memo.pdf | A PDF file; view with xpdf under a GUI |
| memo.ps | A PostScript file; view with gs under a GUI |
| memo.Z | A file compressed with compress (page 163); use uncompress or gunzip (page 163) to decompress |
| memo.tgz or memo.tar.gz | A tar (page 163) archive of files compressed with gzip (page 163) |
| memo.gz | A file compressed with gzip (page 163); view with zcat or decompress with gunzip (both on page 163) |
| memo.bz2 | A file compressed with bzip2 (page 162); view with bcat or decompress with bunzip2 (both on page 162) |
| memo.html | A file meant to be viewed using a Web browser, such as Firefox |
| photo.gif, photo.jpg, photo.jpeg, photo.bmp, photo.tif, or photo.tiff | A file containing graphical information, such as a picture |

## HIDDEN FILENAMES

A filename that begins with a period is called a *hidden filename* (or a *hidden file* or sometimes an *invisible file*) because ls does not normally display it. The command `ls -a` displays *all* filenames, even hidden ones. Names of startup files (page 192) usually begin with a period so that they are hidden and do not clutter a directory listing. The `.plan` file (page 170) is also hidden. Two special hidden entries—a single and double period (. and ..)—appear in every directory (page 197).

## THE WORKING DIRECTORY

`pwd` While you are logged in on a character-based interface to a Linux system, you are always associated with a directory. The directory you are associated with is called the *working directory* or *current directory*. Sometimes this association is referred to in a physical sense: “You are in (or *working in*) the jenny directory.” The `pwd` (print working directory) utility displays the pathname of the working directory.

## YOUR HOME DIRECTORY

When you first log in on a Linux system or start a terminal emulator window, your working directory is your *home directory*. To display the pathname of your home directory, use `pwd` just after you log in (Figure 6–4).

When used without any arguments, the ls utility displays a list of the files in the working directory. Because your home directory has been the only working directory you have used so far, ls has always displayed a list of files in your home directory. (All the files you have created up to this point were created in your home directory.)

### STARTUP FILES

*Startup files*, which appear in your home directory, give the shell and other programs information about you and your preferences. Frequently one of these files tells the shell what kind of terminal you are using (page 1040) and executes the `stty` (set terminal) utility to establish the erase (page 139) and line kill (page 139) keys.

Either you or the system administrator can put a shell startup file containing shell commands in your home directory. The shell executes the commands in this file each time you log in. Because the startup files have hidden filenames, you must use the `ls -a` command to see whether one is in your home directory. A GUI has many startup files. Usually you do not need to work with these files directly but can control startup sequences by using icons on the desktop. See page 281 for more information about startup files.

```
login: alex
Password:
Last login: Wed Oct 20 11:14:21 from bravo
$ pwd
/home/alex
```

![](img/f28adb66a7398a382f0505e0ba74a872_232_0.png)

## PATHNAMES

This section discusses absolute and relative pathnames and explains how to use them to your advantage.

## ABSOLUTE PATHNAMES

Every file has a pathname. Figure 6-5 shows the pathnames of directories and ordinary files in part of a filesystem hierarchy. An absolute pathname always starts with a slash (/), the name of the root directory. You can then build the absolute pathname of a file by tracing a path from the root directory through all the intermediate directories to the file. String all the filenames in the path together, separating each from the next with a slash (/) and preceding the entire group of filenames with a slash (/). This path of filenames is called an **absolute pathname** because it locates a file absolutely by tracing a path from the root directory to the file. The part of a pathname following the final slash is called a *simple filename*, *filename*, or *basename*.

## TILDE (~) IN PATHNAMES

In another form of absolute pathname, the shell expands the characters *~/* (a tilde followed by a slash) at the start of a pathname into the pathname of your home directory. Using this shortcut, you can display your *.bashrc* startup file (page 281) with the following command, no matter which directory is your working directory:

```
$ less ~/.bashrc
```

A tilde quickly references paths that start with your or someone else's home directory. The shell expands a tilde followed by a username at the beginning of a pathname into the pathname of that user's home directory. For example, assuming he

![](img/f28adb66a7398a382f0505e0ba74a872_233_0.png)
