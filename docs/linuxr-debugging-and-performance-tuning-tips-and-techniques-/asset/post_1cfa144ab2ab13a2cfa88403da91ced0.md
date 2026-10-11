
the group. However, for this program, we know there are members, or `print_group()` wouldn’t have been called! Here’s what happens when the program is run:

```
$ ch06-groupInfo arnold
mail:x:12:mail,postfix,arnold
uucp:x:14:uucp,arnold
floppy:x:19:arnold
devel:x:42:miriam,arnold
arnold:x:2076:arnold
```

### 6.4 Terminals: `isatty()`

The Linux/Unix standard input, standard output, standard error model discourages the special treatment of input and output devices. Programs generally should not need to know, or care, whether their output is a terminal, a file, a pipe, a physical device, or whatever.

However, there are times when a program really does need to know what kind of a file a file descriptor is associated with. The `stat()` family of calls often provides enough information: regular file, directory, device, and so on. Sometimes though, even that is not enough, and for interactive programs in particular, you may need to know if a file descriptor represents a tty.

A tty (short for Teletype, one of the early manufacturers of computer terminals) is any device that represents a terminal, that is, something that a human would use to interact with the computer. This may be either a hardware device, such as the keyboard and monitor of a personal computer, an old-fashioned video display terminal connected to a computer by a serial line or modem, or a software *pseudoterminal*, such as is used for windowing systems and network logins.

The discrimination can be made with `isatty()`:

```
#include <unistd.h>
int isatty(int desc);
```

This function returns 1 if the file descriptor `desc` represents a terminal, 0 otherwise. According to POSIX, `isatty()` may set `errno` to indicate an error; thus you should set `errno` to 0 before calling `isatty()` and then check its value if the return is 0. (The GNU/Linux `isatty(3)` manpage doesn’t mention the use of `errno`.) The POSIX standard also points out that just because `isatty()` returns 1 doesn’t mean there’s a human at the other end of the file descriptor!

One place where `isatty()` comes into use is in modern versions of `ls`, in which the default is to print filenames in columns if the standard output is a terminal and to print them one per line if not.

### 6.5 Suggested Reading

- *Mastering Algorithms With C*, by Kyle Loudon. O’Reilly & Associates, Sebastopol, California, USA, 1999. ISBN: 1-56592-453-3.

  This book provides a practical, down-to-earth introduction to algorithms and data structures using C, covering hash tables, trees, sorting, and searching, among other things.

- *The Art of Computer Programming Volume 3: Sorting and Searching*, 2nd edition, by Donald E. Knuth. Addison-Wesley, Reading Massachusetts, USA, 1998. ISBN: 0-201-89685-0.

  This book is usually cited as the final word on sorting and searching. Bear in mind that it is considerably denser and harder to read than the Loudon book.

- The GTK+ project<sup>6</sup> consists of several libraries that work together. GTK+ is the underlying toolkit used by the GNU GNOME Project.<sup>7</sup> At the base of the library hierarchy is Glib, a library of fundamental types and data structures and functions for working with them. Glib includes facilities for all the basic operations we’ve covered so far in this book, and many more, including linked lists and hash tables. To see the online documentation, start at the GTK+ Documentation Project’s web site,<sup>8</sup> click on the “Download” link, and proceed to the online version.

### 6.6 Summary

- Times are stored internally as `time_t` values, representing “seconds since the Epoch.” The Epoch is Midnight, January 1, 1970 UTC for GNU/Linux and Unix systems. The current time is retrieved from the system by the `time()` system call, and `difftime()` returns the difference, in seconds, between two `time_t` values.
- The `struct tm` structure represents a “broken-down time,” which is a much more usable representation of a date and time. `gmtime()` and `localtime()` convert `time_t` values into `struct tm` values, and `mktime()` goes in the opposite direction.
- `asctime()` and `ctime()` do simplistic formatting of time values, returning a pointer to a fixed-size, fixed-format `static` character string. `strftime()` provides much more flexible formatting, including locale-based values.
- Time-zone information is made available by a call to `tzset()`. Since the standard routines act as if they call `tzset()` automatically, it is rare to need to call this function directly.
- The standard routine for sorting arrays is `qsort()`. By using a user-provided comparison function and being told the number of array elements and their size, `qsort()` can sort any kind of data. This provides considerable flexibility.
- `scandir()` reads an entire directory into an array of `struct dirent`. User-provided functions can be used to select which entries to include and can provide ordering of elements within the array. `alphasort()` is a standard function for sorting directory entries by name; `scandir()` passes the sorting function straight through to `qsort()`.
- The `bsearch()` function works similarly to `qsort()`. It does fast binary searching. Use it if the cost of linear searching outweighs the cost of sorting your data. (An additional API for searching data collections is described in Section 14.4, “Advanced Searching with Binary Trees,” page 551.)
- The user and group databases may be kept in local disk files or may be made available over a network. The standard API purposely hides this distinction. Each database provides both linear scanning of the entire database and direct queries for a user/group name or user/group ID.
- Finally, for those times when `stat()` just isn’t enough, `isatty()` can tell you whether or not an open file represents a terminal device.

### Exercises

1. Write a simple version of the `date` command that accepts a format string on the command line and uses it to format and print the current time.
2. When a file is more than six months old, `ls -l` uses a simpler format for printing the modification time. The file `GNU version of ls.c` uses this computation:

```
3043     /* Consider a time to be recent if it is within past six
3044     month.    A Gregorian year has 365.2425 * 24 * 60 * 60 ==
3045     31556952 seconds on the average.    Write this value as an
3046     integer constant to avoid floating point hassles.    */
3047     six_months_ago = current_time - 31556952 / 2;
```

Compare this to our example computation for computing the time six months in the past. What are the advantages and disadvantages of each method?
3. Write a simple version of the `touch` command that changes the modification time of the files named on the command line to the current time.
4. Add an option to your `touch` command that accepts a date and time specification on the command line and uses that value as the new modification time of the files named on the command line.
5. Add another option to your version of `touch` that takes a filename and uses the modification time of the given file as the new modification time for the files named on the command line.
6. Enhance `ch06-sortemp.c` to sort a separate array of pointers that point into the array of employees.
7. Add options to `ch06-sortdir.c` to sort by inode number, modification time, access time, and size. Add a “reverse option” such that time-based sorts make the most recent file first and other criteria (size, inode) sort by largest value first.
8. Write a simple version of the `chown` command. Its usage should be

```
chown user[:group] files ...
```

Here, *user* and *group* are user and group names representing the new user and group for the named files. The *group* is optional; if present it is separated from the *user* by a colon.

To test your version on a GNU/Linux system, you will have to work as *root*. Do so carefully!
