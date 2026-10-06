```
one two four five
$ echo ${mytest[2]}

$ echo ${mytest[3]}
four
$
```

This example uses the unset command to remove the value at index value 2. When you display the array, it appears that the other index values dropped down one. However, if you specifically display the data at index value 2, you'll see that location is empty.

Finally, you can remove the entire array by using the array name in the unset command:

```
$ unset mytest
$ echo ${mytest[*]}

$
```

Sometimes variable arrays are just complicada matters, so they're often not used in shell script programming. They're not very portable to other shell environments, which is a downside if you lots of shell programming for different shells. There are a couple of bash system environment variables that use arrays (such as BASH_VERSION), but overall you probably won't run into them very often.

# Using Command Aliases

While not environment variables per se, shell aliases behave in the same manner. A command alias allows you to create an alias name for common commands (along with their parameters) to help keep your typing to a minimum.

Most likely your Linux distribution has already set some common aliases for you. To see a list of all, use the alias command with the -p parameter:

```
$ alias -p
alias 1.=ls -d * --color=tty
alias 11=ls -l --color=tty
alias 1s=ls --color=tty
alias vi=vim
alias which='alias | /usr/bin/which --tty-only--read-
alias show--dot --show-tilde'
$
```

Notice that on my Linux distribution, they use an alias to override the standard ls command. It automatically provides the --color parameter, indicating that the terminal supports color mode de listings.