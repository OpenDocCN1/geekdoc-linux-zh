An **acconfig.h** file, as a minimum, should contain the package and version definitions. It also can include other things to be defined. Each one is named on an **#undef** statement. You will find that some of the other #undef definitions must be present for the make file generation to succeed. The following shows the contents of an **acconfig.h** file that is close to the minimal requirements:

```
```c
/* acconfig.h */
#undef ENABLE_NLS
#undef HAVE_CATGETS
#undef HAVE_GETTEXT
#undef HAVE_LC_MESSAGES
#undef HAVE_STPCPY
#undef HAVE_LIBSM

#undef PACKAGE
#undef VERSION
```
```

# # The **autogen.sh** Script

You need to create a script with the name **autogen.sh** in your directory. There is another script by this name in the macros directory, but the two are quite different. The one in the macros directory is quite extensive and does all the detailed work of generating the make files. The one you create in your directory does some simple validation and executes the one that is in the macros directory.

```
```bash
#!/bin/sh
# Run this to generate all the initial makefiles, etc.

srcdir=`dirname $0`
test -z "$srcdir" && srcdir=.

PKG_NAME="Hello Auto"

(test -f $srcdir/configure.in \\
 && test -f $srcdir/IDLGBIBLE \\
 && test -d $srcdir/helloauto) || {
    echo -n "**Error**: Directory `\`$srcdir\`""
    echo " does not look like the"
    echo " helloauto development directory"
    exit 1
}

. $srcdir/macros/autogen.sh
```
```

The environment variable **srcdir** is set to the current directory. The variable **PKG_NAME** is used to assign a name to the entire package\u2014that is, a name for the