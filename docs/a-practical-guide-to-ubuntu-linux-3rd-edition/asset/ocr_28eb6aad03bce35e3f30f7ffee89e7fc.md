```
$ cat bb2
set "$0"
echo $@ parameters with "$0" 
echo 1: $1
echo 2: $2
echo 3: $3

$ ./bb2 a b c
3 parameters with "$0" 
1: a
2: b
3: c
```

# Expanding Null and Unset Variables

The expression \$[name] (or just \$name if it is not ambiguous) expands to the value of the *name* variable. If *name* is null or not set, *bash* expands \$[name] to a null string. The *Bourne Again Shell* provides the following alternatives to accepting the expanded null string as the value of the variable:

+   - Use a default value for the variable.
+   - Use a default value and assign that value to the variable.
+   - Display an error.

You can choose one of these alternatives by using a modifier with the variable name. In addition, you can use `set -o nounset` (page 355) to cause *bash* to display an error and exit from a script whenever an unset variable is referenced.

# :− Uses a Default Value

The `:-` modifier uses a default value in place of a null or unset variable while allowing a nonnull variable to represent itself:

```
$[name:-default]
```

The shell interprets `:-` as “If *name* is null or unset, expand *default* and use the expanded value in place of *name*; else use *name*.” The following command lists the contents of the directory named by the `LIT` variable. If `LIT` is null or unset, it lists the contents of /home/max/literature:

```
$ ls ${LIT:-/home/max/literature}
```

The default can itself have variable references that are expanded:

```
$ ls ${LIT:~$HOME/literature}
```

# := Assigns a Default Value

The `:=` modifier does not change the value of a variable. However, you can change the value of a null or unset variable to its default in a script by using the `:=` modifier:

```
$[name:=default]
```