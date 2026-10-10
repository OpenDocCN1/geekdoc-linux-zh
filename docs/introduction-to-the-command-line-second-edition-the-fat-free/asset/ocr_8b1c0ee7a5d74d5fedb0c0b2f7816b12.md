# # make

Purpose: Compile and install software from source code.

Usage syntax: `make [OPTIONS] [FILE]`

```
# ls -l Makefile
-rw-r-- 1 nick nick 1636 2007-08-10 13:48 Makefile
# make 66 make install

*** Stopping make sense ***
make[1]: Entering directory '/home/nick/Desctop/chkrootkit-0.48'
gcc -DHAVE_LASTLOG_H -o chklastlog chklastlog.c
chklastlog.c: In function 'main':
chklastlog.c:167: warning: format '%ld' expects type 'long int', but
option 3 has type 'int'
chklastlog.c:167: warning: format '%ld' expects type 'long int', but
option 4 has type 'uid_t'
gcc -DHAVE_LASTLOG_H -o chkxtmp chkxtmp.c
...
```

![](bbox=[0.27, 0.44, 0.74, 0.47])

The `make` command compiles and installs programs from source code. Source code compatible with the `make` command is distributed with what is known as a Makefile. The Makefile is a script used to build and install the source code using the `make` command.

In the above example, the `make` and `make install` commands are combined to build the source code of a program and install it.

> Most users will never have to compile software from source since major distributions provide prebuilt packages for nearly every program available. Additionally, Linux tools such as yum, apt, and eme greatly simplify software installation and dependency fulfillment.

Common usage examples:

+   - **make** Compile source code
+   - **make install** Install compiled source code