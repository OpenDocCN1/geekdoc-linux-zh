# EXAMPLE 8.66

```
(From SVR4 Shutdown Program)
1 eval `/usr/bin/id | /usr/bin/sed 's/[^a-z0-9=].*/'"
2 if [ "$uid"-0 -ne 0 ]
3 then
    echo $0: Only root can run $0
    exit 2
fi
```

# EXPLANATION

1 This is a tricky one. The id program's output is sent to sed to extract the uid part of the string. The output for id is
uid=9496(e11e) gid=40 groups=40
uid=0(root) gid=1(daemon)

The sed regular expression reads: Find any character that is not a letter, number, or an equal sign and remove that character and all characters following it. The result is to substitute everything from the first opening parenthesis to the end of the line with nothing. What is left is either uid=9496 or uid=0.

After eval evaluates the command line, it then executes the resulting command:
uid=9496
or
uid=0

For example, if the user's ID is root, the command executed would be uid=0. This creates a local variable in the shell called uid and assigns 0 to it.

2 The value of the uid variable is tested for 0, using command modifiers.

3 If the uid is not 0, the echo command displays the script name ($0) and the message.

# 8.10 Shell Invocation Options

When the shell is started using the sh command, it can take options to modify its behavior. See Table 8.7.

# Table 8.7 Shell Invocation Options

| Option | Meaning |
|---|---|
| -i | Shell is in the interactive mode. QUIT and INTERRUPT are ignored. |
| -s | Commands are read from standard input and output is sent to standard error. |
| -c string | Commands are read from string. |