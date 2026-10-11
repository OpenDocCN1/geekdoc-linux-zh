# startx

This `startx` command is actually a script that sets several variables and finally calls the `xinit` application. The following is an example of a `startx` script with comments.

```
```sh
#!/bin/sh
#
# (c) 1999 Red Hat Software, Inc.
bindir=/usr/X11R6/bin
userclientrc=$HOME/.xinitrc
userserverrc=$HOME/.xserverrc
sysclientrc=/etc/X11/xinit/.xinitrc
sysserverrc=/etc/X11/xinit/xserverrc
clientargs=""
serverargs=""
```

```

This sets several variables that point to other script files that get called later.

```
```sh
if [ -f $userclientrc ]; then
    clientargs=$userclientrc
else if [ -f $sysclientrc ]; then
    clientargs=$sysclientrc
fi
fi

if [ -f $userserverrc ]; then
    server=$userserverrc
else if [ -f $sysserverrc ]; then
    server=$sysserverrc
fi
fi
```

```

These lines do a `test -f` check to see if the files in the previous variables exist. The next section, omitted here, executes the script files stored in the variables. These are the `xinitrc` and `xserverrc` files.

```
```sh
# set up default Xauth info for this machine
mcookie=`mcookie`
serverargs="$serverargs -auth $HOME/.Xauthority"
xauth add $display . $mcookie
xauth add `hostname -f` $display . $mcookie
```

```

This block sets up the X security information by executing `xauth`. The `xauth` tool is covered in more detail later in this chapter.

```
```sh
xinit $clientargs -- $server $display $serverargs
```

```

Finally, the `startx` script executes `xinit`.