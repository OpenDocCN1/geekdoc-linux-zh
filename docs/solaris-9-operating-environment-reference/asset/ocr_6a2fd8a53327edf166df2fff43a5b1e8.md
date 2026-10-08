# 36

# alias, unalias

**Note** — If you set aliases in your .profile file, only the login shell has access to them unless you use the -x option to export them. Any shell you invoke after you log in—such as those in xterms or an Windows environment—will not have exported aliases defined.

To create a Korn ENV file, create a file named filename and put your aliases in it. Then export the environment file with the following command:

```
ENV=filename; export ENV
```

# Options

# Korn Shell

The Korn shell provides the options for the built-in alias command.

+   -t Create a tracked alias. The Korn shell remembers the full path name of the command to enable it to be found more quickly and to be issued from any directory. If you supply no alias-name argument, list all currently tracked aliases.

+   -x Export the alias so that it can be used in scripts and other subshells. If you supply no alias-name argument, list all current exported aliases.

The following option is supported by unalias.

+   -a Remove all alias definitions from the current shell execution environment.

# Operands

The following operand is supported for the alias command.

+   alias-name Write the alias definition to standard output.

The following operands are supported for the unalias command:

+   alias-name The name of an alias to be removed.

+   alias-name=string Assign the value of string to the alias alias-name.

When you specify no operands, all alias definitions are written to standard output.

# Output

The format for displaying aliases (when no operands or only name operands specified) is:

```
"%s=%s\n" name, value
```

The valuestring is written with appropriate quoting so that it is suitable for reininput to the shell.