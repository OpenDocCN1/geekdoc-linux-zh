# # The CVS modules file

# Three different line formats are valid:
# key -a aliases...
# key [options] directory
# key [options] directory files...

# Where "options" are composed of:
# -i prog Run "prog on "cvs commit" from top-level module.
# -o prog Run "prog on "cvs checkout" of module.
# -t prog Run "prog on "cvs rtag" of module.
# -u prog Run "prog on "cvs update" of module.
# -d dir Place module in directory "dir" instead of module name.
# -1 Top-level directory only do not recurse.

# And "directory" is a path to a directory relative to CVSROOT.
# The "-a" option specifies alias. An alias is interpreted if
# everything on the right of the "-a" had been typed on the command line.

# You can encode a module within a module by using the special '&'
# character to interpose another module into the current module. This
# can be useful for creating a module that consists of many directories
# spread out over the entire source repository.

# Convenient aliases
world -a

```
# CVSROOT support; run mkmodules whenever anything changes.
CVSROOT -i mkmodules CVSROOT
modules -i mkmodules CVSROOT modules
logininfo -i mkmodules CVSROOT logininfo
commitinfo -i mkmodules CVSROOT commitinfo
rcsinfo -i mkmodules CVSROOT rcsinfo
editinfo -i mkmodules CVSROOT editinfo
```

# Add other modules here...
testgen testgen
testdatal testdatal
testdata2 testdata2
testdata3 testdata3
testdata4 testdata4
testcode testgen/_code
cvs cvs