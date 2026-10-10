
together also issues another signal for the double-click. In this example, two events generate three signals.

Events also come from the X window manager whenever there is some sort of change on the display. An event is issued whenever a window first appears, becomes hidden, changes size, becomes visible, is closed, or is moved. These all translate into signals and are made available to your applications.

There are also signals that originate inside widgets. Whenever it is moved, a scrollbar issues a signal with the information on its new position. A list issues a signal indicating which of its members the mouse selected. A toggle button indicates its state whenever it is turned on or off. A toolbar sends a signal to indicate that its orientation has changed from horizontal to vertical.

All of these signals are available to your program. All you have to do is tell the widget which signal you wish to receive, and what function is to be called to receive it. Because the widget calls you, the function is known as a callback function.

## Enter glib of GIMP

There is a graphics utility program named GIMP (GNU Image Manipulation Program) that is distributed with most, if not all, Linux systems. The developers of GIMP created glib so they could simplify and standardize their software development. This library contains data type definitions, macros, data structures, and a large collection of utility function calls. The items from glib are used to create the GDK, GTK+, and GNOME libraries. This makes it very convenient for you to use them to create your application—in fact, there are some GTK+ and GNOME function calls that require a glib data type as an argument.

## The Fundamental Data Types

There are a number of data types defined in glib. This is a matter of standardization and portability. The size of an int may be 16 bits on one machine and 32 bits on another. Also, a char may be unsigned on one system and signed on another. For example, if your code uses gint32 instead of int, and gchar instead of char, your source code has a much better chance of being portable across platforms.

![](img/8bcc1ba72831c7d67cfc8b395deab95f_38_0.png)

> You will find inconsistencies in the code. There are places, for example, where an int is used interchangeably with a gint. Since programmers all have their own style, and there are a lot of programmers involved in developing open-source software, things are bound to vary a bit. This is a small price to pay for the amazing amount and quality of software produced by the open-source process.

All of the primitive type definitions begin with the prefix letter g. An unsigned integer always begins with the prefix gu. This program lists all the primitive types and sizes:

```c
/** gshow.c **/
#include <glib/gprintf.h>
#include <stdlib.h>

int main(int argc, char *argv[])
{
    g_print("gchar: %d\n", sizeof(gchar));
    g_print("guchar: %d\n", sizeof(guchar));
    g_print("gint8: %d\n", sizeof(gint8));
    g_print("guint8: %d\n", sizeof(guint8));
    g_print("gshort: %d\n", sizeof(gshort));
    g_print("gushort: %d\n", sizeof(gushort));
    g_print("gint16: %d\n", sizeof(gint16));
    g_print("guint16: %d\n", sizeof(guint16));
    g_print("gint: %d\n", sizeof(gint));
    g_print("guint: %d\n", sizeof(guint));
    g_print("gint32: %d\n", sizeof(gint32));
    g_print("guint32: %d\n", sizeof(guint32));
    g_print("glong: %d\n", sizeof(glong));
    g_print("gulong: %d\n", sizeof(gulong));
    g_print("gint64: %d\n", sizeof(gint64));
    g_print("guint64: %d\n", sizeof(guint64));
    g_print("gfloat: %d\n", sizeof(gfloat));
    g_print("gdouble: %d\n", sizeof(gdouble));
    g_print("gpointer: %d\n", sizeof(gpointer));
    g_print("gconstpointer: %d\n", sizeof(gconstpointer));
    g_print("gboolean: %d\n", sizeof(gboolean));
    exit(0);
}
```

The following is a makefile that can be used to compile this program. The gnome-config utility is used to set the environment necessary to compile and link GNOME programs. This process is described in detail in Chapter 2.

```makefile
CC=gcc
LDLIBS=`gnome-config --libs gnomeui`
CFLAGS=-Wall -g `gnome-config --cflags gnomeui`

gshow: gshow.o
	$(CC) $(CFLAGS) -o gshow gshow.o $(LDLIBS)
```

The definitions with names that end with the numbers 8, 16, 32, and 64 are the same length regardless of which platform is used. The other definitions may be different lengths (as defined by the C language). The 64-bit integers gint64 and guint64 are the ones declared in C as long long. When the program is run on an x586 based version of Linux, the output looks like this:

```text
gchar:           1
guchar:          1
gint8:           1
guint8:          1
gshort:          2
gushort:         2
gint16:          2
guint16:         2
gint:            4
guint:           4
gint32:          4
guint32:         4
glong:           4
gulong:          4
gint64:          8
guint64:         8
gfloat:          4
gdouble:         8
gpointer:        4
gconstpointer:   4
gboolean:        4
```

Table 1-2 lists the definition names of the maximum and minimum values contained in some of the data types. There are also some macros defined, as shown in Table 1-3.

| Data Type | Minimum | Maximum |
| :--- | :--- | :--- |
| **gshort** | G_MINSHORT | G_MAXSHORT |
| **gint** | G_MININT | G_MAXINT |
| **glong** | G_MINLONG | G_MAXLONG |
| **gfloat** | G_MINFLOAT | G_MAXFLOAT |
| **gdouble** | G_MINDOUBLE | G_MAXDOUBLE |

### Table 1-3
### Some Useful Macros

| Macro | Description |
| :--- | :--- |
| ABS(a) | The positive value of a is returned. |
| MAX(a,b) | The numeric values a and b are of the same data type, and the macro returns the larger of the two. |
| MIN(a,b) | The numeric values a and b are of the same data type, and the macro returns the smaller of the two. |
| NULL | This is the address value assigned to a pointer to signify that it points to nothing. |
| TRUE and FALSE | There are many functions that require a gboolean type for an argument. One of these names can be used to pass a constant representing either a true or false condition. Also, if you write a function that returns a gboolean type, it can return one of these names. |

## Utility Functions of glib

This section introduces some of the functions that you will encounter throughout the code—and probably use throughout your application. There are many more functions than the ones I list here, but these are the ones you will encounter in GDK, GTK+, and GNOME source code. Also, you will find a few of them in the example code in this book and, because they can be so handy, you may want to use them yourself.

The functions listed here fall roughly into three categories: memory management, string manipulation, and textual output. There is some overlap among them—for example, a string duplication function may need to allocate memory.

### g_free(gpointer mem)

The previously allocated block of memory at mem is returned to the system.

### g_print(gchar *format,...)

This function is analogous to the standard C function print(). It sends the format string to the standard output after inserting into it the other values passed as arguments.

### g_printerr(gchar *format,...)

This function sends the format string to standard error after inserting into it the other values passed as arguments.

### gchar *g_strconcat(gchar *,...)

Memory is allocated that is sufficient to hold all the strings passed in as arguments, the strings are concatenated into it, and its address is returned.

### gchar *g_strdup(gchar *str)

This function allocates the memory necessary to hold the string, copies the string into the new memory, and returns its address.

### gchar *g_strdup_printf(gchar *format,...)

Memory is allocated to hold a new string. The string is created according to the format (along with the optional data items) and a pointer to its address is returned.

### gchar *g_strerror(gint errnumber)

When a C system call or standard C library call encounters an error condition, it stores the error code in the global value `errno`. This function converts the error number to a descriptive string.

### gchar *g_strndup(gchar *str,gint num)

Memory is allocated that is large enough to hold a string of `num` characters, `str` is copied into it, and its address is returned.

### gint g_str_equal(gchar *s1,gchar *s2)

This function returns `TRUE` if `s1` is identical to `s2`.

### gint g_strcasecmp(gchar *str1,gchar *str2)

This function performs a caseless compare (that is, *A* is equal to *a*) and returns `TRUE` if the strings are found to be identical.

### gpointer g_malloc(gulong size)

This function allocates a new block of memory of `size` bytes and returns its address.

### gpointer g_malloc0(gulong size)

This function allocates a new block of memory of `size` bytes, initializes it to zero, and returns its address.

### gpointer g_mempdup(gpointer mem,guint size)

The pointer `mem` is the address of `size` bytes. A new block of memory of the same size is allocated, the contents of `mem` is copied into it, and its address is returned.
