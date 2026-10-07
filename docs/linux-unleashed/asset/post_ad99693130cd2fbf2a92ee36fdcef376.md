
# # ADABAS-D and other Databases

991

## CHAPTER 62

FlagShip uses the curses toolkit for its user interface. During installation, you get a set of terminfo files specifically for FlagShip. When running a FlagShip program in an xterm, you may get hieroglyphics instead of line drawing characters. Fiddling with the asci parameter in the fslnxterm terminfo entry may not help. Try using the vga font that comes with DOSEmu package.

FlagShip doesn't have a function specifically for managing pull-down menus. What FlagShip and Clipper programmers normally do is use @PROMPT/MENU TO statements to create the horizontal menu and a function called @CHOICE() for the vertical menus. You can set hot keys with the SET KEY keyid TO statement. Normally, the statement would be a function invocation. Within this function, you can call the READVAR() function to find out which field the cursor was in when the key was pressed. An input field can be validated by adding the VALID statement parameter to the @SAY/GET statement. Again, the statement would normally be a function invocation. Within the function, the value the user typed in could be looked up in a database file.

FlagShip has functions for managing windows that work very nicely, but the functions are not part of the basic package. You have to buy the FStools library. As the name suggests, the FStools library is a clone of the Clipper Tools library. There are also windowing functions in the NanForum library (containing mathematical and statistics functions), which is public domain.

A key feature of FlagShip is the TBROWSE() object. You use this in place of the BROWSE command that exists in other languages. If you don't have any previous experience with object-oriented programming, setting up TBROWSE() for the first time is not easy. The best course of action is to use the examples and samples in the fsmal pages. FlagShip is picky about reserved words. If you have a filename such as browse, you are liable to encounter problems running programs. Keep a list of all the reserved words in FlagShip and avoid using these as file or program names. Check the list of reserved words in the fsmal pages.

FlagShip programs can be attached to WWW pages, making it possible for net surfers to access and update databases. This feature, plus the capability to link in your C and C++ programs, makes FlagShip a very powerful data management tool.

FlagShip has an online reference program called fsmal, which contains the entire FlagShip manual of more than 1,000 pages, which means that you do not have thick manuals all over your desk. The samples of code in the manual can be saved as text files on disk. This makes it easy to incorporate programming examples in the manual into whatever program you are working on at the time. Of course, you could also use the mouse to copy text from fsmal into your program by cutting and pasting between windows.

FlagShip isn't just a port of a DOS-based compiler. It has been designed to provide full functionality under UNIX. Source code will run faster under Linux than under DOS (compiler with Clipper, for example) because of the better operating system design of Linux. FlagShip also removes many of the limitations of DOS- and Windows-based xBase applications.

If you have any requirement to port dBASE or Clipper applications to Linux, or you are looking for a simple relational database system, FlagShip is an excellent choice.

### Installing FlagShip

Most people obtain FlagShip from a CD-ROM collection, a Web site, or an FTP archive. In most cases, there are two versions of FlagShip available, and the choice of the correct one for your system depends on the version of Linux you are running. Typically, the files are contained in a tar archive called fsdemo.tar (if you are obtaining the restricted demo version). One version is optimized for more recent releases of Linux and uses ELF. An older version, usually designated with the name aout (for a.out) at the end of the file-name, works on any Linux system. The ELF version is much more flexible and powerful, but in most cases the demo files are the older version.

Once you have the fsdemo.tar file on your Linux system in a suitable (preferably new and empty other than the fsdemo file) directory, you need to unpack the tar file with the command:

```
tar xvf fsdemo.tar
```

This creates a number of files, two of which are usually called F$install.set and F$install. The F$install.set file sets environment variables for the installation routine and should be run first by simply typing its name at the command line. You won't see anything when you do this. After running the .set file, type the F$install filename and let it install FlagShip for you.

If the installation process loads properly, you are asked if there is enough room on your filesystem, as shown in Figure 62.1.

#### FIGURE 62.1.

The FlagShip installation routine checks that you have enough room on your hard drive.

![](img/e8e6b47ac20475e23d48b4c476f5d891_1028_0.png)

You are then asked where you want the FlagShip program to be stored, and in most cases you should accept the default values suggested by the installation routine. If you want to change the defaults, a menu prompt lets you, and then enter the new values, as shown in Figure 62.2. Once the installation routine has finished, you are returned to the shell prompt. FlagShip is now ready to be used.

#### FIGURE 62.2.

You can override the default FlagShip installation settings if you want.

![](img/e8e6b47ac20475e23d48b4c476f5d891_1028_1.png)

### Using FlagShip

If you have used Clipper or one of the other xBase compilers, you will know most of the commands you need for FlagShip. A few modifications have been made because of the UNIX environment, but using FlagShip is otherwise pretty simple. Keep in mind that FlagShip is not an interactive development product: it doesn’t help you design your code. FlagShip is a compiler. You can use it to develop applications if you are familiar with the dBASE language, but FlagShip is not designed to teach you dBASE or to help you develop applications.

Once you have your .prg source files ready to go, you can invoke the FlagShip compiler. In general, the command line is like this...

```
FlagShip app_name.prg -ocompiled_name -Mstart
```

...where app_name.prg is the name of the main program file (that calls all the others) and compiled_name is the name of the compiled executable (C defaults to a.out as the compiled executable name). If your main program file doesn't call all the other program files that need to be linked together, you will have to compile them separately and link them together.

Once compiled, the application runs as though it were on DOS or any other operating system. For example, Figure 62.3 shows a DOS application that has been ported to Linux and recompiled with FlagShip, and then executed. The only changes necessary to the source code were changes in path names from DOS's structure to Linux's. As you can see, even the fundamental ASCII graphics are retained and can be used on any terminal supported by Linux.

#### FIGURE 62.3.

A FlagShip-compiled application runs under Linux just as it would under DOS.

![](img/e8e6b47ac20475e23d48b4c476f5d891_1029_0.png)

### Porting Existing Applications

What do you have to worry about if you have some existing dBASE or Clipper code that you want to run under Linux? To start with, you need the .prg (program) source code. Move those files to Linux using any means you want, such as a network connection or floppy disk. FlagShip is clever enough to ignore case, which may seem trivial but isn't. Since most DOS programmers write in mixed case, converting applications to run under UNIX's case-significant environment is a major problem with other dBASE tools.

There are complete instructions on modifying code to run cleanly under FlagShip included with the software (or available through the FlagShip Web page), but essentially most applications can run straight away.

FlagShip converts dBASE code into C source code and then compiles it with a C compiler. That means you will need a C compiler, which luckily is part of almost every UNIX and Linux system available. If you want to use FlagShip and haven't installed the C development system from the CD-ROM, you should do so; otherwise, you will see error messages from FlagShip. You don't need C++, only the standard C compilers that
