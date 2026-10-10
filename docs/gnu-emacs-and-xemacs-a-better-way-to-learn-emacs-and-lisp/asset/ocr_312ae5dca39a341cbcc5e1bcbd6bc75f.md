Now load the newly-created makefile into an Emacs session, and look near the top of the file for this section:

```
```
##################################################
#
# user configurable parameters
#

prefix=/usr

# LIB_DIR should be a private place for notes-mode stuff.
LIB_DIR=$(prefix)/share/notes-mode

# EL_DIR should be where your site-specific emacs .el[.c]s go.
EL_DIR=/usr/share/emacs/site-lisp
# INFO_DIR is for emacs info files.
INFO_DIR=$(prefix)/info
INSTALL_INFO=/usr/sbin/install-info
# must be perl 5.000 or better.
PERL=/usr/bin/perl
# must be 19 or greater
EMACS=emacs
MKDIR_P=mkdir -p
#
       !
# end of user configurable parameters
#
##################################################
```
```

Check to see if the parameters accurately reflect how you want the package installed. Make any necessary changes and save the file to disk.

XEmacs users need to make one extra edit; change this line:

```
`EMACS=emacs`
```

to this:

```
`EMACS=xemacs`
```

This assumes that the XEmacs executable is in your path. Otherwise, type in the path as well—something like this:

```
`EMACS=/opt/bin/xemacs`
```

Now that the makefile is ready, you can type

```
`make install`
```