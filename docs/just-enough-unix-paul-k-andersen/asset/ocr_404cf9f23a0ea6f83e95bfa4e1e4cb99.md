G.2  Running make

The first thing to do with make is to remove the executable and object files that were produced when you compiled the Trip program the first time. Try the 1s command to see the files in Trip:

```
$ ls (Return)
```

You should see something like this:

```
a.out    indiana.c    indy.o     main.o
chicago.c  indiana.o    main.c    makefile
chicago.o  indy.c
```

Now get rid of the old object files:

```
$ make clean (Return)
```

The "clean" dependency line in makefile causes the following command line to run:

```
rm *.o
```

Use the 1s command now to list the files remaining in Trip:

```
$ 1s (Return)
```

You should see:

```
a.out    indiana.c    main.c
chicago.c  indy.c     makefile
```

Note that make did nothing to the old executable file a.out, because it was not instructed to do so.

Next, use make to compile the program. Simply type make and press (Return):

```
$ make (Return)
```

make then follows the instructions in makefile to compile the program:

```
cc -c main.c
cc -c chicago.c
cc -c indiana.c
cc -c indy.c
cc -o trip main.o chicago.o indiana.o indy.o
```

Note that the files are not necessarily compiled in exactly the same order as they appear in makefile; instead, make figures out which files should be compiled first. Try the 1s command to see the files in Trip:

```
$ 1s (Return)
```