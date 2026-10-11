
# Chapter 10 — C Programming with db

```c
int main(void)
{
	DB *db;
	DBC *dbc;
	DBT key, value;
	int ret;

	ret = db_open("test.db", DB_BTREE,
			DB_CREATE, 0600, NULL, NULL, &db);
	if(ret) {
		perror("dbopen");
		exit(EXIT_FAILURE);
	}

	/* Create a cursor */
	ret = db->cursor(db, NULL, &dbc, 0);
	if(ret) {
		perror("cursor");
		exit(EXIT_FAILURE);
	}
	memset(&key, 0, sizeof(key));
	memset(&value, 0, sizeof(value));

	/* Move sequentially through the database */
	while((ret = dbc->c_get(dbc, &key, &value,
		DB_NEXT)) != DB_NOTFOUND) {
		printf("key/value is %s/%s\n", (char *)key.data,
			(char *)value.data);
	}

	/* Sync the database */
	db->sync(db, 0);

	/* Close the cursor */
	dbc->c_close(dbc);

	db->close(db, 0);
	exit(EXIT_SUCCESS);
}
```

The output from this program follows:

![](img/be588b36b489136ce784030a08a1d3d4_246_0.png)

### Output

```
$ ./cursor
key/value is five/Signals
key/value is four/Processes
key/value is one/Compiling Programs
key/value is three/About the Project
key/value is two/Controlling the Build Process
```

As you can see, marching sequentially through the database, the records are, in fact, stored in sorted order based on the record key. After opening the database and creating a cursor, the program continually calls `c_get` to retrieve the next record from the database and then displays both the key and its associated value. When `c_get` returns `DB_NOTFOUND`, there are no more records to retrieve. The `sync` call is not actually necessary because no data has been changed, but it is included to illustrate its use. Note also that `cursor` closes the database cursor, `dbc`, before it closes the database. Although it is not strictly required, it is a good habit to develop to make sure that all resources allocated by the DB interface are properly returned to the operating system.

> **NOTE**
> Although not discussed, I used the program addmore.c, also on the Web site, to add records to the database. It is part of the makefile for this chapter, so you can build it to complete this example. It prompts you to enter five records at a time.

### What's Next?

This chapter introduced you to the Berkeley database, the first of several Linux APIs you will learn. The next two chapters show you how to use ncurses to control the appearance of character-mode screens. You will also learn to interact with mice, create menus, and draw forms.

# 11 — Screen Manipulation with ncurses

This chapter introduces ncurses (pronounced "en-curses"), the free implementation of the classic UNIX screen-handling library, curses. ncurses provides a simple, high-level interface for screen control and manipulation. It also contains powerful routines for handling keyboard and mouse input, creating and managing multiple windows, and using menus, forms, and panels. Topics this chapter include the following:

- ncurses capabilities
- Terminology and concepts
- Initialization and termination routines
- Character and string output
- Character and string input

### ncurses Features

ncurses, which is short for "new curses," is a freely redistributable clone of the curses libraries distributed with the System V Release 4.0 (SVR4) of UNIX distributed by Bell Labs. The name "curses" is derived from the phrase "cursor optimization," which succinctly describes what curses does.

### Terminal Independence

ncurses generalizes the interface between an application program and the screen or terminal on which it is running. Given the literally hundreds of varieties of terminals and screens, in particular the different features they possess and the commands to invoke them, UNIX programmers needed a way to abstract screen manipulation. Rather than write a lot of extra code to take into account the different terminal types, ncurses provides a uniform and generalized interface for the programmer. The ncurses API insulates the programmer from the underlying hardware.

### Capabilities

ncurses gives to character-based applications many of the same features found in graphical X Window applications: multiple windows, forms, menus, and panels. ncurses' windows can be managed independently, may contain the same or different text, may or may not scroll, and can be hidden. The vi editor and the popular file manager Midnight Commander are written using ncurses.

Forms enable the programmer to create easy-to-use data entry and display windows, thus simplifying what is usually a difficult and application-specific coding task. Panels extend curses' capability to deal with overlapping and stacked windows. Menus, which give the user a simple interface by invoking application options, are easily implemented using ncurses' simple, generalized menu programming interface. The version used in this book is 4.2, although the 5.0 release is currently in beta.

### Compiling with ncurses

To compile a program with ncurses, you need its function and variable definitions, so include `<curses.h>` in your source code:

```c
#include <curses.h>
```

Many Linux systems make `/usr/include/curses.h` a symbolic link to `/usr/include/ncurses.h`, so you could conceivably include `<ncurses.h>`. However, for maximum portability, use `<curses.h>` because, believe it or not, ncurses is not available on all UNIX and UNIX-like platforms. You also need to link against the ncurses libraries, so use the `-lcurses` option when linking, or add `-lncurses` to the `LDFLAGS` make variable or the `LDFLAGS` environment variable:

```
$ gcc curses_prog.c -o curses_prog -lcurses
```

By default, debug tracing is disabled in ncurses programs. To enable debugging, link against ncurses’ debug library, `libncurses_g.a`, and either call `trace(N)` in your code or set the environment variable `$NCURSES_TRACE` to N, where N is a positive, non-zero integer. Doing so forces debugging output to a file named, appropriately, `trace`, in the current directory. The larger N’s value, the more detailed, and so more voluminous, the debugging output. Useful values for N are documented in `<ncurses.h>`. For example, the standard trace level, `TRACE_ORDINARY`, is 31.

### Examples

![](img/be588b36b489136ce784030a08a1d3d4_249_0.png)

#### Example

1. This is the simplest possible ncurses program. It merely starts and stops the ncurses subsystem; no output is generated.

```c
/*
 * simple.c Simple ncurses program
 */
#include <curses.h>

int main(void)
{
	initscr();
	endwin();
	return 0;
}
```

![](img/be588b36b489136ce784030a08a1d3d4_249_1.png)

### Output

To compile and execute it, type the following:

```
$ gcc simple.c -o simple -lncurses
$ ./simple
```

2. The next example uses the debugging library and makes a couple of extra function calls to generate output:

![](img/be588b36b489136ce784030a08a1d3d4_249_2.png)

### Example

```c
/*
 * debugit.c ncurses program calling trace()
 */
#include <curses.h>

int main(void)
{
	initscr();
	trace(TRACE_CALLS);
	printw("set debug level to TRACE_CALLS");
	refresh();
	endwin();
	return 0;
}
```

The command line to compile this program is as follows:

```
$ gcc debugit.c -o debugit -lncurses_g
$ ./debugit
```

If you are really fast, you may see the message flash by on the screen! The *trace* call results in every ncurses function call being written to the file *trace* in the current directory. An excerpt of this file is reproduced here:

![](img/be588b36b489136ce784030a08a1d3d4_251_0.png)

### Output

```
TRACING NCURSES version 4.2 (990213)
printw("set debug level to TRACE_CALLS", ...) called
called waddnstr(0x80675f8,"set debug level to TRACE_CALLS",-1)
..., current (A_NORMAL)
return 0
called wrefresh(0x80675f8)
clearing and updating from scratch
ClrDate() called
ClearScreen() called
screen cleared
updating screen from scratch
return 0
TransformLine(0) called
TransformLine(1) called
...
TransformLine(24) called
return 0
called endwin()
return 0
```

> **TIP**
> The ncurses package comes with a script, *tracemunch*, that compresses and summarizes the debug information into a more readable, human-friendly format.
