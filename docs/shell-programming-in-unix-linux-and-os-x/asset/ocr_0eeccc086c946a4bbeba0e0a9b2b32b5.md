# Functions 269

A function definition can continue over as many lines as necessary. The shell will continue to prompt for commands within the function with the secondary command prompt until you complete the function definition with the ).

You can put definitions for commonly used functions inside your .profile so they'll be available whenever you log in. Alternatively, you can group the definitions in a file, say myfuncs, and execute the function in the current shell by typing

+   - myfuncs

As you know now, this causes any functions defined myfuncs to become available in the current shell.

The following function, called mycd, takes advantage of the fact that functions are run in the current environment. It mimics the operation of the Korn shell's cd command, which has the capability of substituting portions of the current directory's path (see the discussion of cd in Chapter 14 for more explanation).

```
$ myfuncs
# See what's inside
# new cd function:
#   mycd switches dir
#   mycd old new  Substitute for old in current directory's path
#
mycd () {
  if [ $# -le 1 ]; then
    # normal case -- 0 or 1 argument
    cd $1
  elif [ $# -eq 2 ]; then
    # special case -- substitute $2 for $1
    cd $$(echo $PWD | sed "s|$1|$2/")
  else
    # mycd can't have more than two arguments
    echo mycd: bad argument count
    exit 1
```

```
fi
```

```
}
```

```
$ .myfuncs  Read in definition
```

```
$pwd
/users/steve
```

```
$ mycd  Change directory
Did it work?
```

```
$users/pat
```

```
$ mycd pat tony  Substitute tony for pat
```

```
$pwd
/users/tony
$
```