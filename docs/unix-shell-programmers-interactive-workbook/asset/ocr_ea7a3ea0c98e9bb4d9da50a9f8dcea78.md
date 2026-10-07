# 360 Lab 7.2: The [[ COMMAND... ]] OPERATOR

In the code we are looking at, z is a single command, the one that prints the "does not exist" message, so the braces around it are omitted because there is no need to "group" a single command.

That takes care of the outer if statement. The inner one, the y part of the code shown here, is a bit more complex. We'll use lowercase letters to differentiate between the following pseudo-code and the code we just looked at.

```
[[ w ]] && { x ; return }\n[[ y ]] && { z ; return }
```

is equivalent to

```
if [[ w ]] then x
elif [[ y ]] then z
fi
```

![](bbox=[0.115, 0.473, 0.215, 0.503])

> Watch out! The return statement takes you out of whatever program you are running, but if you use it from the command line, where no script or function is running, it will take you out of your interactive session with the shell and log you off!

+   d) Could this program have been written as a script instead of as a function?

Answer:Yes it could. Scripts and functions work the same way.

The script version would look like the following:

```
# s722 -- Use [[ instead of if -- script version
[[ -e "$1" ]] && (
  [[ -f "$1" ]] && (
    print "$1" is a regular file.\n    return
  )
  [[ -d "$1" ]] && (
    print "$1" is a directory.\n    return
  )
)
print \"\""$1\"\" does not exist.
```