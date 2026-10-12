
## alias

Syntax:

```
/alias name commands
```

This allows you to create an alias, or a macro, for commonly used commands. This is most useful in your ircII startup and configuration file. However, it can also be used within the client at runtime.

The commands part can consist of just about any ircII command. If you want to string together several commands, you separate them with a semicolon (;).

You can also insert special character sequences, such as ircII variables in the commands part. Such sequences are prefixed with a $. To see the built-in variables that are available in ircII you can use the /help alias special command. There are also special variables for macros that you can use to let the user specify options when running your macros. These option variables are called $0, $1, and so on. Each occurrence of one of these numbered variables will be expanded into the corresponding option that the user supplied with the macro. In some situations you will want the last variable to be set to all the remaining parts of the user input. This can, for example, be useful for a macro where the last part is a message. To accomplish this you will need to add a hyphen (-) after the variable name.

### Note

> Commands used in an alias statement should not be prefixed with a /!

Here is a short example of how to define an alias:

```
/alias reply msg $, $0.
```

The special variable $ expands to the nickname of the user who last sent a message to you. You then use the alias like this:

```
/reply Hi there!
```

This would then be expanded, internally, into the following by ircII (if WSB was the user who last sent a message to you):

```
/msg WSB Hi there!
```

Finally, if you want to remove an alias, you can prefix the name parameter with a hyphen (-).

## away

Syntax:

```
/away message
```

This will mark your status as being “away.” If someone sends you a message or does a /whois on you, he will receive your message in reply.

To remove your away status, simply use the `/away` command once again, this time without supplying a message.

## bye, exit, signoff, and quit

Syntax:

```
/bye reason
/exit reason
/signoff reason
/quit reason
```

All of these commands will terminate your current IRC session. There is no difference between the commands; they are different aliases for the same command. It is possible to supply a sign off reason as a parameter to the commands. For example:

```
/bye Time to rejoin my real life...
```

The previous example would result in the following output to the channel you were in (assuming your nickname on the server was set to WSB):

```
*** Signoff: WSB (Time to rejoin my real life...)
```

## channel and join

Syntax:

```
/channel channels
/join channels
```

The `/channel` command is used to join channels on the IRC net you are currently connected to. This command can either be specified as `/channel` or as `/join`. If no channels are specified you will get a list of those channels that you are currently in.

Channel names can begin with a # or a &. The former are channels that are available on all servers within the IRC net to which you are currently connected. The latter type of channel is only available locally on the server you are connected to. Local channels are not very common. The channel name can consist of any character except space, carriage return, null, and line feed.

If you specify a channel that does not exist, it will be created and you will become the operator for that channel. Being an operator goes outside the scope of this section. However, you can refer to /help to find out more about the commands that are available for a channel operator.

## disconnect

Syntax:

```
/disconnect
```

This command will disconnect you from the server specified. If you don't specify a server, the command will default to the current server.

## dmsg and msg

Syntax:

```
/dmsg nickname message
/msg nickname message
```

This command is used to send a private message to the user with the specified nickname. Only the user with the specified nickname will be shown the message. If you specify `.` as the nickname, the message will be sent to the user to whom you last sent a message.

## help

Syntax:

```
/help command
```

This will show a help section about the given command. The command should be specified without prefixing it with a `/`. At any given moment when using the help command you can issue a `?` to be given a list of available topics and sub-topics.

## leave or part

Syntax:

```
/leave channel
/part channel
```

Use this to leave a channel. If you do not specify a channel name, the client will assume that you want to leave the currently active channel.

## list

Syntax:

```
/list expression
```

The /list command will present you with a list containing various information about the specified channels. In this list you will find channel name, how many users there are in the channel at the moment, and the topic of the channel (if one is set).

If you are in a channel and set the expression to a * character, you will only be shown information about the channel you are currently in. If you are not in a channel when you use a * character as an expression, then all available channels will be listed.

There are several options available for the /list command. These options are enabled by specifying one or several of the various switches together with the command. See Table 7.3 for a summary of the control switches that are available. Using the /list command without any expression or switches can produce quite a lot of output.

If the server you are connected to is under a high load you may not be allowed to run the /list command. If this occurs, you can usually retry the /list command again after a little while.

### Table 7.3 Control Switches for the /list Command

| Switch | Description |
| :--- | :--- |
| -ALL | Overrides previous -PUBLIC and -PRIVATE control switches. |
| -MAX n | Lists only those channels that currently have more than n users. |
| -MIN n | Lists only those channels that currently have fewer than n users. |
| -PRIVATE | Lists only channels that are marked as private. |
| -PUBLIC | Lists only channels that are open for everyone. |
| -TOPIC | Lists only channels that have a topic set. |
| -WIDE | Lists channel information in as little space as possible. This switch may take the following argument to change the sorting order of the list: |
| -NAME | Orders the list by the name of the channels. |
| -USERS | Orders the list by the number of users in each channel. |

## names

Syntax:

```
/names switches channel
```

This command will list the nicknames of all the users in the specified channel. If you do not specify a channel, information for all channels will be listed. To get information only about the channel you currently are in, use a * for channel name. See Table 7.4 for a list of available switches.

### Table 7.4 Control Switches for the /names Command

| Switch | Description |
| :--- | :--- |
| -ALL | Overrides any previous -PUBLIC and/or -PRIVATE switches. |
| -MAX n | Channels with more than n users will not be shown. |
| -MIN n | Channels with fewer than n users will not be shown. |
| -PRIVATE | Only shows channels marked as private. |
| -PUBLIC | Only shows channels that are public. |

## nick

Syntax:

```
/nick nickname
```

This command is used to set your nickname, or nick as it is often abbreviated. If someone else is using the nick you requested, you will be prompted for a new nickname. When you start the ircII client it will use your Linux login name as the default nickname. You can modify this behavior by creating an .ircrc configuration file for ircII.

On some IRC nets it is possible to register and reserve your nickname. Doing this makes sure that you are the only one that can use that nick on that net. This might be a good idea if you are going to use that IRC net a lot. Furthermore, your chat buddies can be reasonably sure that it is really you with whom they are chatting if you have a registered nick.

The behavior of nick registration can be different on different IRC nets. The most common method goes something like this: If you try to set your nickname to one that is already registered by someone else then you will be given 60 seconds to specify another nickname. If you do not change the name within the allotted 60 seconds, the server will change your nickname for you. It will set a nick patterned along the lines of guest<number>. Many IRC channels will not allow people with such a nickname to join them. Therefore, it is always best to change to a proper nickname as quickly as possible.

## server

Syntax:

```
/server servername:port
/server number
```
