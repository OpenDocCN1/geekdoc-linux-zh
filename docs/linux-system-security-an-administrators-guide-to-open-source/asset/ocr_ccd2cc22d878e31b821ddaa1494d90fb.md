# Example 6-4 Creating the S/Key Version 1.1b Executables

```
# make linux
make all SYS=sysv RANLIB="echo" CFLAGS="-g -DSYSV -DPOSIX"
make[1]: Entering directory '/usr/src/skey/src'
cc -g -DSYSV -DPOSIX -c skeylogin.o -o skeylogin.o
cc -g -DSYSV -DPOSIX -c skeysubr.c -o skeysubr.o
cc -g -DSYSV -DPOSIX -c md4.c -o md4.o
cc -g -DSYSV -DPOSIX -c put.c -o put.o
ar rv libkey.a skeylogin.o skeysubr.o md4.o put.o
a - skeylogin.o
a - skeysubr.o
a - md4.o
a - put.o
echo libkey.a
libkey.a
cc -o key -g -DSYSV -DPOSIX skey.c libkey.a
cc -o keyinit -g -DSYSV -DPOSIX skeyinit.c libkey.a -lcrypt
cc -o keysh -g -DSYSV -DPOSIX skeysh.c libkey.a
Make completed.
make[1]: Leaving directory '/usr/src/skey/src'
#
```

# NOTE

You may get an error message of the form

```
/usr/src/skey/src/skeyinit.c:108: undefined reference to `crypt'
```

when you run make 1inux as shown in Example 6-4. This indicates that the library containing the crypt system call was not found. To remedy this situation, edit the Makefile in /usr/src/skey/src (or wherever you put it) and change

```
keyinit: skeyinit.c $(LIB)
$(CC) -o $@ $(CFLAGS) skeyinit.c $(LIB) $(SYSLIBS)
```

to

```
keyinit: skeyinit.c $(LIB)
$(CC) -o $@ $(CFLAGS) skeyinit.c $(LIB) $(SYSLIBS) -lcrypt
```

and try the make 1inux command again.

Now you have the binaries associated with S/Key Version 1.1b. They are

```
key
keyint
keysh
```

The keyint and key programs were described earlier in association with Figure 6.1 on page 120. The keysh program is a replacement login shell. If you specify it instead of the normal /bin/bash or /bin/ksh or other shell, then the user will always get the S/Key challenge. In a PAM environment, this will occur after any of the PAM requirements are met. This is the ubiquitous approach and, again, may or may not be suitable for your environment. More flexible approaches will be outlined later in this chapter.