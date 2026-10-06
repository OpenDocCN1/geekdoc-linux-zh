# 218 Part II + The SUSE System

```
# ./configure
checking for a BSD-compatible install... /usr/bin/install -c
checking whether build environment is sane... yes
checking for gawk... awk
checking whether make sets $(MAKE)... yes
checking for gcc... gcc
checking for C compiler default output name... ...a.out
```

Next, you will need to run the make command. The make command uses the
Makefile created by the configure script to build all of the components of the
Fluxbox window manager in the right order. The following is some sample output
from the command:

```
# make
cd .\
## CONFIG FILES: CONFIG_HEADERS=config.h \
  /bin/sh ./config.status
config.status: creating config.h
config.status: config.h is unchanged
config.status: executing default-1 commands
make all-recursive
```

After completion, you have installed Fluxbox by executing the command
make install using sudo or as the root user. Fluxbox and all of its themes
and other requirements will be installed to the appropriate subdirectories of
/usr/local on your system. The Fluxbox executable is installed as
/usr/local/bin/Fluxbox.

# Using Fluxbox

After you have installed Fluxbox, you will want to experiment with it. The easiest way
to experiment with different window managers on SUSE system is to create a
file called xinitrc (located in your home directory) that starts the X applications
and window manager of your choice. If you are using a graphical display manager
s as kdm (the default on SUSE systems), the specified applications and window
manager will start automatically the next time you log in on your system. If you
are using your system at run level 3 (non-graphical mode), you can start the X
applications and window manager by executing the xinit command from
command line.

First, create a sample .xinitrc in your home directory using your favorite text
editor. A simple .xinitrc file that starts a single terminal (xterm) and application
then starts the Fluxbox window manager is the following:

```
/usr/X11R/bin/xterm &
exec /usr/local/bin/fluxbox
```