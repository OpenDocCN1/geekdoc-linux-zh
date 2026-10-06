# CDPATH

The CDPATH variable works like the PATH variable: it specifies a list of directories to be searched by the shell whenever you execute a cd command. This search is done only if the specified directory is not given by a full pathname and if CDPATH is not null. If you type in

```
cd /users/steve
```

the shell changes your directory directly to /users/steve; but if you type

```
cd memos
```

the shell looks at your CDPATH variable to find the memos directory. And if your CDPATH looks like this:

```
$ echo $CDPATH
::/users/steve:/users/steve/docs
$
```

the shell first looks in your current directory for a memos directory, and if not found looks in /users/steve for a memos directory, and if not found tries /users/steve/docs in a last ditch effort to find the directory. If the directory is not relative to your current one, the cd command prints the full path to the directory to let you know where it's taking

```
$ cd /users/steve
$ cd memos
/users/steve/docs/memos
$ cd bin
/users/steve/bin
$ pwd
/users/steve/bin
$
```

Like the PATH variable, use of the period for specifying the current directory is optional,
:/users/steve:/users/steve/docs

is equivalent to
:/users/steve:/users/steve

Judicious use of the CDPATH variable can save you a lot of typing, especially if your directory hierarchy is fairly deep and you find yourself moving around in it (or if you're frequently moving into other hierarchies as well).

Unlike PATH, you'll probably want to put your current directory first in the CDPATH list. This gives you the most natural use of CDPATH; if the current directory isn't listed, you may end up in an unexpected directory!

Oh, and one more thing: CDPATH isn't set when you log in; you need to explicitly set it to the sequences of directories you'd like the shell to use when searching for the specified name.