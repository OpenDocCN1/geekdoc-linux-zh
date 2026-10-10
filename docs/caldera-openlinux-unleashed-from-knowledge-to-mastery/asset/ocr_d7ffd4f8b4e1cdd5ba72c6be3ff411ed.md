# # The for Statement

The for statement looks like the following:

```
for VAR in WORDS ; do COMMANDS ; done
```

Here, VAR is the name of a shell variable, and WORDS is a list of words. COMMANDS is a list of commands.

To see an example of for in action, type the following:

```
```
$ for X in 1 2 3 4; do echo "I like $X"; done
I like 1
I like 2
I like 3
I like 4
```
```

You can also make a "poor-man's" ls command:

```
```
$ for X in /etc/* ; do echo "$X"; done
/etc/HOSTNAME
/etc/PHI.conf
/etc/X11
...
```
```

# # Built-In Shell Variables and
# Positional Parameters

The shell has several built-in variables. Some are covered in Chapter 3. Table 30.1 lists some built-in variables useful for shell scripting.

TABLE 30.1 Built-in Shell Variables

| Variable | Meaning |
| :------- | :------- |
| **PATH** | Colon-separated list of directories in which the shell searches for commands. |
| **HOME** | Your home directory. |
| **PS1** | The shell’s primary prompt. |
| **PS2** | The shell’s secondary prompt (when it is waiting for more input to complete a command.) |
| **RANDOM** | Each time this variable is read, a random integer is returned. |
| **\*** | A list of all positional parameters passed to a shell script. If enclosed in double quotes, it expands to a single parameter. |
| **@** | A list of all positional parameters passed to a shell script. If enclosed in double- quotes, expands to a list of double-quoted parameters. |