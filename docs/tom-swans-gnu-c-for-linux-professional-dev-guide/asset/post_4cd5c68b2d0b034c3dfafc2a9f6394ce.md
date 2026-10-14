
necessary compiling and linking commands. Before using this Makefile, you might have to modify some of the settings in a related file, Config.mk. Locate that file in the outer directory (src/c26 for this chapter), and load it into your editor. Listing 26.1 shows the Config.mk file's default settings.

## LISTING 26.1 C26/CONFIG.MK

```
# Edit the following for your installation
CC = g++
X11INC = /usr/X11R6/include
X11LIB = /usr/X11R6/lib
LIBS = -lX11

# Compiler and linker flags
CFLAGS = -O -I$(X11INC)
LFLAGS = -O -L$(X11LIB)
```

Edit the first four variables in Config.mk to select the compiler name (CC), X include directory (X11INC), and X compiled library directory (X11LIB). Also specify the Xlib pathname (LIBS) for the GNU linker. The default settings should work for most readers, but if you have trouble compiling, it's likely the compiler can't find the files it needs. In that case, search for your X11 installation directories and make the appropriate adjustments to Config.mk. To compile all programs for loading into the GNU debugger, add -g to CFLAGS.

If you are using Red Hat Linux 5.1 or earlier, you might have to change X11R6 to X11 in the pathnames listed in Config.mk. If so, make this same change to the Config.mk files located in the src/C26, src/C27, src/C28, and src/C29 directories.

After configuring your system, change to a named directory and run the make utility to compile and link a sample program. For example, to compile the xwelcome demonstrator, enter commands such as these:

```
$ cd src/c26/xwelcome
$ make
g++ -c -O -I/usr/X11/include -o xwelcome.o xwelcome.cpp
g++ -o xwelcome -O -L/usr/X11/lib xwelcome.o -lX11
```

The last two lines show the compilation and linking commands issued by make using the commands in Makefile. To run the program, enter its compiled executable filename as follows, prefaced with ./ to tell the shell to look in the current directory:
$ ./xwelcome

If all goes well, that should display the sample window in Figure 26.3. To quit the program, press any key when the program's window is active (that is, when it has the input focus). Most sample programs in this and the next chapters end on sensing a keypress, or they provide a menu command or a button named Exit. You can also click the window's close button, shown by most window managers as a small lowercase x. Another way to end X clients, although unusual, is to switch to the shell window from which you started the program and type C-c (Ctrl-C). However, this might not work with all X applications.

You can also use make and the supplied Makefiles to clean up a directory after you are finished trying out the sample program. To use this feature, enter make clean. Notice that this also removes the compiled executable file:

```
$ make clean
rm -f xwelcome.o
rm -f *~
rm -f xwelcome
```

## Figure 26.3
The xwelcome program's window.

![](img/6eab91cc30158075ed10d0cabbac9029_661_0.png)

## INCLUDING Xlib HEADERS

All X client applications include the Xlib.h header file, usually along with one or two other X declaration files. The xwelcome.cpp sample program includes the following three headers:

```
#include <X11/Xlib.h>
#include <X11/Xutil.h>
#include <X11/Xos.h>
```

Including Xlib.h also includes X.h, and as a result, this declares most data types and structures needed by Xlib programs. The Xutil.h header includes many common X function declarations and is also needed by most X clients. Including Xos.h is optional, but it can help reduce problems caused by system dependencies and differences among declarations in other headers—such as, for instance, the names of various string.h functions and the size of a word data type.

You might find other hardware- or operating-system-dependent include files on a specific installation. For best results, avoid including these files into X clients. There should be no reason to include any header files other than those located in your include/X11 (or X11R6) system directory.

## CONNECTING TO THE X SERVER

The first programming step in every X client is to connect to the X server. If this can't be done, either there is a serious network problem or X simply isn't running. First, declare a global display pointer as follows:

```
Display *display;
```

Because almost all Xlib functions require a reference to a Display structure, the pointer to it is usually made global to avoid having to pass it to the program's subroutines. The first step inside main() initializes the display pointer using statements such as the following:

```
display = XOpenDisplay(NULL);
if (display == NULL) {
  cerr << "Failure connecting to X Server";
  exit(1);
}
```

If XOpenDisplay() fails, it returns NULL. Always check for this condition, and exit the program with an error message if the connection can't be established. There are other ways to call XOpenDisplay(). You can, for example, pass the name of a host and a display number separated by a colon as a string, but these and other possibilities are system-dependent. (The environment variables HOSTDISPLAY and DISPLAY typically specify the correct values.) Passing NULL for Linux XFree86 installations is usually the best choice. Depending on the argument passed to XOpenDisplay(), the connection to the X server may be established locally or across a network.
