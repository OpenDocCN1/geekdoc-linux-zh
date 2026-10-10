```
AM_GNU_GETTEXT

AC_SUBST(CFLAGS)
AC_SUBST(CPPFLAGS)
AC_SUBST(LDFLAGS)

AC_OUTPUT([
Makefile
macros/Makefile
helloauto/Makefile
])
```

# # The Text Files

Table 20-2 lists a number of text files that are stored in the root directory to document the system. You also can find files by these names in the subdirectories that contain source code.

Table 20-2 Some Usual Documentation Files

| File Name | Contains |
| :--- | :--- |
| AUTHORS | The list of names of the software’s authors. Quite often the e-mail addresses are listed also. |
| BUGS | If there is some problem with the code that may cause someone a lot of trouble, it is a good idea to create this file and explain the problem. |
| COPYING | The copyright information. You can find several of these files throughout the source trees of GNOME and GTK+. There are some slight variations in a few of them, so you can copy the one you like and, if you wish, make your own variation. However, if your changes are such that it no longer is GNU, you cannot say that it is. |
| DEPENDS | If the compilation depends on the prior existence of something outside this source tree, such as a special library, you can list it in this file. |
| HACKING | The information listed in this file is for someone who wants to make modifications to the source and compile it. It lists any special utilities or procedures that are required. There often are compile instructions and warnings. |