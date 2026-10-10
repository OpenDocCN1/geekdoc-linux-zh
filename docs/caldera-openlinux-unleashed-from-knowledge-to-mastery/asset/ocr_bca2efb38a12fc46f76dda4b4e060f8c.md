Type the following into a file called functest:

```
max() {
    if test $# = 0 ; then
        echo "??"
        return 1
    fi
    MAX=$1
    for N in "$@"; do
        if test "$N" -gt "$MAX" ; then MAX=$N; fi
    done
    echo "$MAX"
    return 0
}
```

Now source the file by typing: `source functest`. The source command reads the contents of a file as if you had typed them into the shell. Now test the max function:

```
$ max 1 9 8 4
9
$ max
??
```

As you see, the function behaves just like a built-in command. Note that if you do not supply any parameters, the function prints ?? and returns with a status of 1. (I used `return` instead of `exit` to terminate the function. `exit` would log you out of your shell!)

The back-tick quotes are quite useful with shell functions. This example uses the `max` function to compute a value to assign the the variable `VAL`:

```
$ VAL=`max 9 1 8 3 5`
$ echo $VAL
9
```

# Going Further with Shell
Programming

The previous sections have given you a good introduction to shell programming. To go further, read the excellent bash manual and info pages. You should also examine shell scripts to see how they work. All the programs in `/etc/rc.d/init.d` are shell scripts; many of the ones in `/usr/bin` are too. To get a listing of shell scripts in `/usr/bin`, run this command:

```
$ file /usr/bin/* ; grep Bourne
```

Other Bourne-shell derivatives like `zsh` and `ksh` are fairly similar to bash. The C shell family (`tcsh` and `csh`) have completely different programming syntax, but the concepts

![](bbox=[0.83, 0.83, 0.97, 0.99])