Variables can also contain the value of other variables. This is useful when you have to preserve a value that will change so you can use it later in the script. Here `BALANCE` is set to the value of the `CurBalance` variable.

```
BALANCE="$CurBalance"
```

> **NOTE:** When assigning variables, use only the variable name (for example, `BALANCE`). When referenced, meaning you want the value of the variable, precede it with a dollar sign (as in `$CurBalance`). The result of the latter is that you get the value of the string, and not the string itself.

# Special shell variables

There are special variables that the shell assigns for you. The most commonly used variables are called the *positional parameters* or *command line arguments* and are referenced as `$0`, `$1`, `$2`, `$3` . . . `$n`. `$0` is special and is assigned the name used to invoke your script; the others are assigned the values of the parameters passed on the command line. For instance, if the shell script named `myscript` were called as:

```
myscript foo bar
```

the positional parameter `$0` would be `myscript`, `$1` would be `foo`, and `$2` would be `bar`.

Another variable, `$#`, tells you how many parameters your script was given. In our example, `$#` would be 2. Another particularly useful special shell variable is `$?`, which receives the exit status of the last command executed. Typically, a value of zero means everything is okay, and anything other than zero indicates an error of some kind. For a complete list of special shell variables, refer to the *bash man* page.

# Parameter expansion in bash

As mentioned earlier, if you want the value of a variable, you precede it with a `$` (for example, `${CITY}$`). This is really just a shorthand for the notation `${ CITY }` ; curly braces are used when the value of the parameter needs to be placed next to other text without a space. Bash has special rules that allow you to expand the value of a variable in different ways. Going into all the rules is probably a little overkill for a quick introduction to shell scripts, but Table 12-1 presents some common constructs that you’re likely to see in bash scripts you find on your Fedora or RHEL box.