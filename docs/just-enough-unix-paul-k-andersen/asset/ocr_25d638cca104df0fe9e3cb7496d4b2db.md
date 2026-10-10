# # MAINTAINING PROGRAMS WITH MAKE

G.2 *Running make*

You should see something like this:

a.out indiana.c indy.o makefile
chicago.c indiana.o main.c trip
chicago.o indy.c main.o

trip contains the new executable code, which you can run simply by typing *trip*, followed by **Return**:

```
$ trip**Return**
```

The advantage of using *make* to compile the files becomes apparent when you begin making alterations in any of the source files. When you are finished, all you have to do is type *make*, and *make* will automatically recompile only those files that need it. And if you have not made any changes in the program, *make* will take no action. To see how this works, try running *make* again:

```
$ make**Return**
```

Assuming you have not made any changes in the files, you should see a message such as

'trip' is up to date. **Return**