
in with all uppercase, log out and try again in lowercase.

## Task 4.2: Having ls Tell You More

Without options, the ls command offers relatively little information. Questions you might still have about your directory include these: How big are the files? Which are files, and which are directories? How old are they? What hidden files do you have?

- 1. Enter ls -s to find out file sizes:

Click here to view code image

```
% ls -s
 total 563
 1 Archives      1 Mail      5 RUMORS.18Sept   280 mailing.lists
 1 InfoWorld     1 News      1 bin           2 newels
 261 LISTS       1 OWL       4 iecc.list     1 src
```

- 2. To ascertain the size of each file or directory listed, you can use the -s flag with ls. The size indicated is the number of kilobytes, rounded upward, for each file. The first line of the output also indicates the total amount of disk space used, in kilobytes, for the contents of this directory (563 in this case). The summary number does not, however, include the contents of any subdirectories, so it’s deceptively small.

### Note

A kilobyte is 1,024 bytes of information, and a byte is a single character. The preceding paragraph, for example, contains slightly more than 400 characters. Unix works in units of a block of information, which, depending on which version of Unix you’re using, is either 1 kilobyte or 512 bytes. (Solaris, for example, uses 512-byte blocks.) Most Unix systems work with a 1-kilobyte block, however. When you use the -s flag, you’re shown how many of these blocks each file contains.

- 3. Here is a further definition of what occurs when you use the -s flag: ls -s indicates the number of blocks each file or directory occupies. You then can use simple calculations to convert blocks into bytes. For example, the ls command indicates that the LISTS file in my home directory occupies 261 blocks. A quick calculation of block size × number of blocks reveals that the maximum file size of LISTS is 133,632 bytes.

You can always estimate size by multiplying the number of blocks by 1,000. Be aware, however, that in large files, the difference between 1,000 and 1,024 is significant enough to introduce an error into your calculation. As an example, bigfile is more than 3 megabytes in size (a megabyte is 1,024 kilobytes, which is 1,024 bytes, so a megabyte is 1,024×1,024, or 1,048,576 bytes):

```
% ls -s bigfile
 3648 bigfile
```

- 4. The file actually occupies 3,727,360 bytes. If I estimated its size by multiplying the number of blocks (3,648, as seen in the output of the preceding command) by 1,000

(which equals 3,648,000 bytes), I’d have underestimated its size by 79,360 bytes. (Remember, blocks × 1,000 is simply an easy estimate!)

### Note

The preceding example reveals something else about the ls command: You can specify individual files or directories you’re interested in viewing and avoid having to see all files and directories in your current location.

### Note

Depending on what shell you’re using and what version of Unix you have, you might be able to press the Tab key while typing in a filename and have it automatically completed if it’s unambiguous. Try it; if you have this shortcut, it’s great!

5. You can specify as many files or directories as you like, and you separate them with spaces:

Click here to view code image

```
% ls -s LISTS iecc.list newels
261 LISTS        4 iecc.list      2 newels
```

In the preceding hour, you learned that Unix identifies each file that begins with a dot (.) as a hidden file. Your home directory is probably littered with dot files, which retain preferences, status information, and other data. To list these hidden files, use the -a flag to ls:

Click here to view code image

```
% ls -a
.           .gopherrc   .oldnewsrc  .sig        RUMORS.18Sept
..          .history    .plan       Archives    bin
.Agenda     .info       .pnewsexpert InfoWorld   iecc.list
.aconfigrc  .letter     .report     LISTS       mailing.lists
.article    .login      .rm-timestamp Mail        newels
.cshrc      .mailrc     .rnlast     News        src
.elm        .newsrc     .rnsoft     OWL
```

You can see that this directory contains more dot files than regular files and directories. This is not uncommon in a Unix home directory. However, it’s rare to find any dot files other than the standard dot and dot-dot directories (which are in every directory in the entire file system) in directories other than your home directory. (These dot files are typically created by applications you use, and they should be edited only with care.)

6. You used another flag to the ls command—the -F flag—in the preceding hour. Do you remember what it does?

Click here to view code image

```
% ls -F
Archives/   Mail/       RUMORS.18Sept mailing.lists
InfoWorld@  News/       bin/        newels
LISTS       OWL/        iecc.list   src/
```
