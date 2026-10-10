subdirectory of the site-lisp directory named auctex and install the files there. This isn’t absolutely necessary, but it is helpful to keep the many files AUCTeX installs in one place rather than mix them up with other site-lisp files.

The section of the makefile that needs to be changed is near the beginning and looks like this:

```
```
##-------------------------------
## YOU MUST EDIT THE FOLLOWING LINES
##-------------------------------

# Where local software is found
prefix=/usr/local

# Where info files go.
infodir = $(prefix)/info

# Where local lisp files go.
lispdir = $(prefix)/share/emacs/site-lisp

# Where the AUC Tex emacs lisp files go.
auctdir=$(lispdir)/auctex

# Name of your emacs binary
EMACS=emacs
```
```

Edit these lines so that they reflect your Emacs installation, and then (from a terminal window) run the *make* command after switching to the directory that contains the unarchived AUCTeX files. Just type

```
```make
make
```
```

The makefile invokes Emacs in noninteractive mode. The result is that the AUCTeX Lisp files will be byte-compiled by your version of Emacs. When this process is finished, type

```
```make
make install
```
```

The files will be copied to the directory you specified in the makefile.

One last step, and you will be ready to use the package. Insert this line into your `~/.emacs` file:

```
```lisp
(require 'tex-site)
```
```

The next time you start Emacs, load a `*.tex` file. The AUCTeX menus should appear.