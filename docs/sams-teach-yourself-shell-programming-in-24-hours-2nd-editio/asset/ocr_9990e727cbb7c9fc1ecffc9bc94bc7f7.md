# Recursion

In the previous section, you learned about the concept of function chaining, where one function calls another function. Recursion is a special instance of function chaining in which a function calls itself. The following example illustrates the use of recursion:

```
reverse() {
  if [ $# -gt 0 ]; then
    typeset arg=$1
    shift
    reverse "$@"
    echo "$arg "
  fi
}
reverse "$@"
```

This script prints its arguments in reverse order. It does so by calling the function reverse with $@ as its arguments. The reverse function is really simple; it determines whether there are any arguments. If there are no arguments, the function does nothing. Otherwise, it saves the first argument, removes it from the argument list using shift and calls itself. Once this call returns, the function just prints the argument it saved.

If you name the script reverse.sh and execute it with the arguments a b c, as follows:

```
#!/bin/sh

readPass () {
  PASS=''           # clear password
  echo -n "Enter Password: "  # print the prompt
  stty -echo        # turn off terminal echo to prevent peeping!
  read PASS         # read the password
  stty echo         # restore terminal echo
  echo              # printout a new line to make output nice
}

readPass
echo Password is $PASS
```

The output is
c
b
a

![](bbox=[0.15, 0.9, 0.25, 0.97])

> In the previous example, you executed the script using /bin/sh. This will not work on Solaris and SunOS systems. On those systems, you need to execute the script using /bin/ksh rather than /bin/sh as /bin/sh on Solaris does not support the typeset command.