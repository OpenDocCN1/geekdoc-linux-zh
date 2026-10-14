
instructions here. (You can use the following commands to install other files such as a program written in C++, or development source code files.)

After downloading a "tarred and zipped" file, you need to unpack it into a directory. Always create a temporary directory for this purpose to prevent accidentally installing a few hundred files in your home or other directory. After unpacking, look for Readme or similarly named files for additional instructions.

Note

> MS-DOS and Microsoft Windows users who download Linux and UNIX files might find their filenames scrambled. This happens because Microsoft operating systems do not like filenames with multiple extensions. One solution is to rename your files—for example, from filename.tar.gz to filename-tar.gz (the hyphen may also be an underscore). If you copy a "tarred and zipped" file from a DOS or Windows directory to a Linux directory, you might find the filename truncated to something like file-1.gz. In that case, note the original filename and use the Linux mv command to rename the file before proceeding.

To decompress and unpack a "tarred and zipped" file, copy it to an empty directory, and then enter commands such as the following:

```
$ gunzip gcc-g++-2.95_1.tar.gz
$ tar -tf gcc-g++-2.95_1.tar
$ tar -xvf gcc-g++-2.95_1.tar
```

The first command decompresses the file and automatically removes the .gz filename extension. The second command, which you can skip if you want, lists the tarred files before unpacking them. The third command unpacks the files and creates any necessary subdirectories. You don't have to type the full filenames—just type the first few letters and press Tab to complete the names automatically (assuming that your shell supports this feature).

At this point, you need to look for a Readme or other file containing compilation and additional installation instructions. In many cases, you merely need to set up a configuration file, and then run the make utility to compile and copy files to their final resting places. (If you have trouble, check the Web sites listed in Appendix C, "Web and FTP Sites," for help. Look for FAQ sheets and other online help files.)

## Caldera OpenLinux Users

If you are using Caldera's OpenLinux, especially version 2.2, you might discover that the automated installation does not properly install the GNU C++ compiler. This is so even if you select the option All Recommended Packages. Following is an email message from this book's technical editor, Richard Blum, describing the problem and explaining the steps he took to resolve it. Perhaps his account will help you install GNU C++ if you experience the same difficulty. Rich writes...

> "I decided to upgrade to Caldera OpenLinux 2.2. After a couple of failed attempts, I was finally able to get it running on my PC. When I tried to compile the first program, I received a 'command not found' error. I checked, and sure enough, g++ was not on the system. The GNU C compiler, gcc, was installed and worked fine, but not g++. I checked the installed programs, and the egcs c++ module was not loaded (even though I had selected the Install All Packages option). I tried to manually install the package, but RPM claimed that it failed on 'dependencies.' Thinking that I must have seriously messed something up, I reinstalled the entire

The first command decompresses the .gz file and removes the filename extension. The second command unpacks the archive using the Linux tar utility and creates all chapter subdirectories such as C04 and C05. After unpacking the files, you can remove the original archive, unmount the CD-ROM, and if you are logged in as the super user, return to a normal user by issuing these commands:

```
$ umount /mnt/cdrom
$ exit
$ cd /home/yourname
$ rm gplsrc.tar
```

You can now change to a chapter subdirectory and compile the programs found there (in some cases, you might have to look further into other subdirectories to find listing files):

```
$ cd src/c04
$ g++ welcome.cpp
$ ./a.out
```

## COMPARING C AND C++

C programmers reading this book might want to hunt for information specific to C++. Following is a list of key differences between C and C++ that will help you focus on the topics you need to learn to begin programming "the C++ way." Beginners and newcomers to C and C++ can skip this section, which uses terms familiar to C programmers but not yet introduced in this book. You might find the following information useful also for upgrading C programs to C++, or just for deciphering a C program's source code statements:

- C and C++ generally use the same syntax, operators, expressions, built-in types, structures, arrays, unions, loops, functions, and pointers. These fundamental elements are used identically in both languages.

- C and C++ support the same kinds of preprocessor directives such as #include, #define, and conditional expressions such as #ifdef.

- C++ has several new reserved words (a total of 97 in my version of GNU C++), many of which are the same in C and C++. See Chapter 6, "Creating Data Objects," and also Appendix A, "GNU C++ Reserved Words," for a complete list of GNU C++ reserved words.

- C++ introduces a few operators that are not found in C. For example, the "put-to" operator << is used to write data to objects. This book fully explains how to use all C and C++ operators. See Appendix B, "C++ Operator Precedence and Associativity," for a complete list.

- C++ supports minimum and maximum operators. The expression (X <? Y) returns the lesser of X and Y. The expression (X >? B) returns the greater of X and Y. Not all C++ compilers support this feature.

- C++ requires all functions to have formal prototypes. C encourages, but does not require, function prototypes. Functions that are used before being declared (that is, if there are any implicit function declarations) generate a compiler error.
