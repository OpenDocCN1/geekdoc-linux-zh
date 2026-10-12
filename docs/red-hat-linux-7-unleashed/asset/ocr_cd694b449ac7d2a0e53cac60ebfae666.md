# alias

Syntax:

```
/alias name commands
```

This allows you to create an alias, or a macro, for commonly used commands. This is most useful in your ircII startup and configuration file. However, it can also be used within the client at runtime.

The commands part can consist of just about any ircII command. If you want to string together several commands, you separate them with a semicolon (;).

You can also insert special character sequences, such as ircII variables in the commands part. Such sequences are prefixed with a $. To see the built-in variables that are available in ircII you can use the /help alias special command. There are also special variables for macros that you can use to let the user specify options when running your macros. These option variables are called $0, $1, and so on. Each occurrence of one of these numbered variables will be expanded into the corresponding option that the user supplied with the macro. In some situations you will want the last variable to be set to all the remaining parts of the user input. This can, for example, be useful for a macro where the last part is a message. To accomplish this you will need to add a hyphen (-) after the variable name.

# Note

> Commands used in an alias statement should not be prefixed with a /!

Here is a short example of how to define an alias:

```
/alias reply msg $, $0.
```

The special variable $ expands to the nickname of the user who last sent a message to you. You then then use the alias like this:

```
/reply Hi there!
```

This would then be expanded, internally, into the following by ircII (if WSB was the user who last sent a message to you):

```
/msg WSB Hi there!
```

Finally, if you want to remove an alias, you can prefix the name parameter with a hyphen (-).