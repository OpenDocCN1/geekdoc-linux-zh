```
############################################################
## Just a 'make' generates a help message
help Help:
  @echo "You can make the following:"
  @echo " "
  @echo "libbuf.a -- the buffer library"
  @echo "bufdisplay -- any-format buffer"
  @echo "buf2pm -- convert buffer to pixmap"
############################################################
```

```
# The main target is the library
libbuf.a: $(OBJS)
t-/bin/rm libbuf.a
ar vr libbuf.a $(OBJS)
ranlib libbuf.a
############################################################
```

```
# Secondary targets -- utilities built from the library
bufdisplay: bufdisplay.c -o bufdisplay $(BUFLIB) $(XLDLIBS)
$((CC) $(CFLAGS) bufdisplay.c -o bufdisplay
buf2pm: buf2pm.c libbuf.a
$((CC) $(CFLAGS) buf2pm.c -o buf2pm $(BUFLIB)
```

```
############################################################
## Build the individual object units
buff.o: $(INCLUDES) buff.c
$((CC) -c $(CFLAGS) buff.c
```

```
buff_print.o: $(INCLUDES) buff_print.c
$((CC) -c $(CFLAGS) buff_print.c
```

```
xtbuff.o: $(INCLUDES) $(XINCLUDES) xtbuff.c
$((CC) -c $(CFLAGS) xtbuff.c
```

The make utility can be used for tasks other than compiling code. As a final example, assume that you have a database that has IP addresses and the corresponding hostnames in two columns that the database dumps these values to a file named hosts.tab. You need to extract only the hostnames from this file and generate a Web page named hosts.html containing these names. The following Makefile is a simple report writer:

```
$ cat makefile
#
SHELL=/bin/sh
#
```

```
hosts.html: hosts.tab
  @echo "<html><body>" > hosts.html
  @awk '{print $2, "br>"}' hosts.tab >> hosts.html
```