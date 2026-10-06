You could make your current directory by typing `cd $M`. You could run a program from that directory called hotdog by typing `$M/hotdog`. You could edit a file from there called by typing `vi $M/bun`.

# Adding Aliases

Aliases can save you even more typing than setting environment variables. With aliases, you can have a string of characters execute an entire command line. You can add and list aliases with the `alias` command. Here are some examples:

```
alias p='pwd' ; ls -CF'
alias rm='rm -i'
```

In the first example, the letter `p` is assigned to run the command `pwd`, and then it runs `ls -CF` to print the current working directory and its contents in column. The second runs `rm` command with the `-i` option each time you simply type `rm`. (This is an alias that is set automatically for the root user, so that instead of just removing files, you are prompted for each individual file removal. This prevents you from removing all the files in a directory by mistakenly typing something as `rm *`).

While you are in the shell, check which aliases are set by typing the `alias` command. If you want to remove an alias, type `unalias`. (Remember that the `alias` is in a configuration file, it will be set again when you open another shell.)

# Using Environment Variables

Every active shell stores pieces of information that it needs to use in what are called environment variables. An environment variable can store things such as locations of configuration files, mailboxes, and path directories. You can also store values for your shell prompts, the size of your history list, and type of operating system.

To see the environment variables currently assigned to your shell, type the `declare` command. (It will probably fill more than one, so type `declare I more.`.) You can refer to the value of any of those variables by preceding it with a dollar sign (`$`) and placing it anywhere on a command line. For:

```
echo USER
chris
```

This command prints the value of the `USER` variable, which holds your username (chris). Substitute any other value for `USER` to print its value instead.