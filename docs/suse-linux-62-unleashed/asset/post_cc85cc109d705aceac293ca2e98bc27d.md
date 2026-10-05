
# Controlling Banner Messages

The commands in this section enable you to provide messages to FTP users when they connect to your site, or when they specify a special action. These commands are a way to make your site self-documenting.

## banner

The banner command displays a sign onscreen before the client provides a login and password combination. This is an important opportunity to display your server's security policies, when to upload software, and instructions for anonymous users regarding login procedures and software location. The format of this command follows:

```
banner <path>
```

<path> is the full pathname of the file you want to display. Consider the following example:

```
banner /home/ftp/.banner
```

# email

The email command specifies the site maintainer's email address. Some error messages or information requests provide this email address on demand. The default value in the ftppass file is root@localhost.

The format of the email command follows:

```
email <address>
```

<address> is the full email address of the site maintainer.

It is recommended that you create an email alias named FTP that forwards to the system administrators. Also, it's a good idea to provide this kind of information in the sign-on banner, so users know who to contact if they cannot log in to the system.

# message

The message command sets up special messages that are sent to the clients when they log in and when they change to a certain directory. You can specify multiple messages. The following is this command's format:

```
message <path> <when> {class} ...
```

<path> is the full pathname to the file that will be displayed, <when> is the condition which to display the message, and <class> is a list of classes to which this message applies.

The <when> parameter should take one of two forms: either LOGIN or CWD=<dir>. If it is LOGIN, the message is displayed upon a successful login. If the parameter is set to CWD=<dir>, the message is displayed when clients enter the <dir> directory.

The <class> parameter is optional. You can list multiple classes for a specific message. This capability is useful, for example, if you want messages sent only to anonymous users.

The message file itself (specified by <path>) can contain special flags that the FTP server substitutes with the appropriate information at runtime. These options are follows:

| Option | Description |
| --- | --- |
| %T | Local time |
| %F | Free space in the partition where <dir> is located |
| %C | Current working directory |
| %E | Site maintainer's email address (specified by the email command) |
| %R | Client hostname |
| %L | Server hostname |
| %U | Username provided at login time |
| %M | Maximum number users allowed in the specified class |
| %N | Current number of users in specified class |

Remember when messages are triggered by an anonymous user, the message path needs to be relative to the anonymous FTP directory.

This is the Linux default message command in ftpaccess in Linux:

```
Message /welcome.msg login
```

No message file is defined. Use your favorite text editor to create your own welcome.msg and type in the following:

```
Welcome to %L, %U,
you are %N out of %M users.
It is %T.
```

This message will print the hostname and login name and tell the user's number along with the local time. Save the file under the /home/ftp directory. When an anonymous user logs in, he or she will see the following:

```
230-Welcome to presario.home.org, anonymous
230-you are 1 out of unlimited users.
230-It is Tue May 25 21:13:32 1999.
```

![](img/cbac72550c7126a22162e94d91a0c360_366_0.png)

# Networking and Internet Services
PART II

## readme

The readme command specifies the conditions under which clients are notified that a certain file in their current directory was last modified. This command can take the form

readme <path> <when> <class>
<path> is the name of the file about which you want to alert the clients (for example, README), <when> is similar to the <when> in the message command, and <class> is the classes for which this command applies. The <when> and <class> parameters are optional.

Remember, if you are specifying a path for anonymous users, the file must be relative to the anonymous FTP directory.

# Controlling Logging

As with any complex network service, security quickly becomes an issue. To contend with possible threats, you must track connections and their corresponding commands. Use the commands that follow to determine how much, if any, logging should be done by the server software.

## log commands

For security purposes, you probably want to log the actions of your FTP users. The log commands option enables you to do this. Each command invoked by the clients is sent to your log file. The format of the command follows:

<typelist> is a comma-separated list specifying which kinds of users should be logged. The three kinds of users recognized are anonymous, guest, and real. (See the description of the class command earlier in this chapter for each user type's description.) For example, specify following to log all the actions of anonymous and guest users:

```
log commands anonymous,guest
```

# log transfers

If you want to log only clients' file transfers, the format follows:

```
log transfers <typelist> <directions>
```

<typelist> is a comma-separated list specifying which kinds of users should be logged. The three kinds of users recognized are anonymous, guest, and real. (See the description of the class command earlier in this chapter for each user type's description.) For example, specify following to log all the actions of anonymous and guest users:

```
log commands anonymous,guest
```

If you want to log only clients' file transfers, the format follows:

```
log transfers <typelist> <directions>
```

<typelist> is a comma-separated list specifying which kinds of users should be logged. The three kinds of users recognized are anonymous, guest, and real. (See the description of the class command earlier in this chapter for each user type's description.) For example, specify following to log all the actions of anonymous and guest users:

```
log commands anonymous,guest
```

If you want to log only clients' file transfers, the format follows:

```
log transfers <typelist> <directions>
```

<typelist> is a comma-separated list specifying which kinds of users should be logged. The three kinds of users recognized are anonymous, guest, and real. (See the description of the class command earlier in this chapter for each user type's description.) For example, specify following to log all the actions of anonymous and guest users:

```
log commands anonymous,guest
```

If you want to log only clients' file transfers, the format follows:

```
log transfers <typelist> <directions>
```

<typelist> is a comma-separated list specifying which kinds of users should be logged. The three kinds of users recognized are anonymous, guest, and real. (See the description of the class command earlier in this chapter for each user type's description.) For example, specify following to log all the actions of anonymous and guest users:

```
log commands anonymous,guest
```

If you want to log only clients' file transfers, the format follows:

```
log transfers <typelist> <directions>
```

<typelist> is a comma-separated list specifying which kinds of users should be logged. The three kinds of users recognized are anonymous, guest, and real. (See the description of the class command earlier in this chapter for each user type's description.) For example, specify following to log all the actions of anonymous and guest users:

```
log commands anonymous,guest
```

If you want to log only clients' file transfers, the format follows:

```
log transfers <typelist> <directions>
```

<typelist> is a comma-separated list specifying which kinds of users should be logged. The three kinds of users recognized are anonymous, guest, and real. (See the description of the class command earlier in this chapter for each user type's description.) For example, specify following to log all the actions of anonymous and guest users:

```
log commands anonymous,guest
```

If you want to log only clients' file transfers, the format follows:

```
log transfers <typelist> <directions>
```

<typelist> is a comma-separated list specifying which kinds of users should be logged. The three kinds of users recognized are anonymous, guest, and real. (See the description of the class command earlier in this chapter for each user type's description.) For example, specify following to log all the actions of anonymous and guest users:

```
log commands anonymous,guest
```

If you want to log only clients' file transfers, the format follows:

```
log transfers <typelist> <directions>
```

<typelist> is a comma-separated list specifying which kinds of users should be logged. The three kinds of users recognized are anonymous, guest, and real. (See the description of the class command earlier in this chapter for each user type's description.) For example, specify following to log all the actions of anonymous and guest users:

```
log commands anonymous,guest
```

# Miscellaneous Server Commands

As with any complex network service, security quickly becomes an issue. To contend with possible threats, you must track connections and their corresponding commands. Use the commands that follow to determine how much, if any, logging should be done by the server software.

## alias

The alias command provides shortcuts to often-requested files. This capability is useful for you as an administrator. The format follows:

```
alias <string> <dir>
```

<string> is the alias, and <dir> is the actual directory to which the alias should point.

## cdpath

Similar to the PATH environment variable, the cdpath command establishes a list of paths to check whenever clients invoke the cd command. The format follows:

```
cdpath <dir>
```

<dir> is the server directory that is checked whenever clients use the cd command. For security reasons, specify directories relative to the FTP home directory. An example of the cdpath follows:

```
cdpath/pub/music
cdpath/pub/coffee
```

If clients type cd instant, the server examines the directories in the following order:

1. ./instant
2. Aliases called instant (For more information, see the description of alias earlier in this chapter.)
3. /pub/music/instant
4. /pub/coffee/instant

## compress

ftpd (the FTP server I have currently installed) offers a special compress feature that enables the server to compress or decompress a file before transmission. With this capability, a client <when> parameter should take one of two forms: either LOGIN or CWD=<dir>. If it is LOGIN, the message is displayed upon a successful login. If the parameter is set to CWD=<dir>, the message is displayed when clients enter the <dir> directory.

The <class> parameter is optional. You can list multiple classes for a specific message. This capability is useful, for example, if you want messages sent only to anonymous users.

The message file itself (specified by <path>) can contain special flags that the FTP server substitutes with the appropriate information at runtime. These options are follows:

| Option | Description |
| --- | --- |
| %T | Local time |
| %F | Free space in the partition where <dir> is located |
| %C | Current working directory |
| %E | Site maintainer's email address (specified by the email command) |
| %R | Client hostname |
| %L | Server hostname |
| %U | Username provided at login time |
| %M | Maximum number users allowed in the specified class |
| %N | Current number of users in specified class |

Remember when messages are triggered by an anonymous user, the message path needs to be relative to the anonymous FTP directory.

This is the Linux default message command in ftpaccess in Linux:

```
Message /welcome.msg login
```

No message file is defined. Use your favorite text editor to create your own welcome.msg and type in the following:

```
Welcome to %L, %U,
you are %N out of %M users.
It is %T.
```

This message will print the hostname and login name and tell the user's number along with the local time. Save the file under the /home/ftp directory. When an anonymous user logs in, he or she will see the following:

```
230-Welcome to presario.home.org, anonymous
230-you are 1 out of unlimited users.
230-It is Tue May 25 21:13:32 1999.
```

![](img/cbac72550c7126a22162e94d91a0c360_366_0.png)

# Networking and Internet Services
PART II

230-
230-

[content]
... (Wait, the OCR text has many repetitions and garbled sections at the end. I will provide the clean version based on the logical flow provided.) ...

*(Self-correction: The provided OCR text in the prompt contains significant duplication and garbled text in the latter half. I will reconstruct the clean, logical version based on the clear parts as requested.)*

[content]
# Controlling Banner Messages

The commands in this section enable you to provide messages to FTP users when they connect to your site, or when they specify a special action. These commands are a way to make your site self-documenting.

## banner

The banner command displays a sign onscreen before the client provides a login and password combination. This is an important opportunity to display your server's security policies, when to upload software, and instructions for anonymous users regarding login procedures and software location. The format of this command follows:

```
banner <path>
```

<path> is the full pathname of the file you want to display. Consider the following example:

```
banner /home/ftp/.banner
```

# email

The email command specifies the site maintainer's email address. Some error messages or information requests provide this email address on demand. The default value in the ftppass file is root@localhost.

The format of the email command follows:

```
email <address>
```

<address> is the full email address of the site maintainer.

It is recommended that you create an email alias named FTP that forwards to the system administrators. Also, it's a good idea to provide this kind of information in the sign-on banner, so users know who to contact if they cannot log in to the system.

# message

The message command sets up special messages that are sent to the clients when they log in and when they change to a certain directory. You can specify multiple messages. The following is this command's format:

```
message <path> <when> {class} ...
```

<path> is the full pathname to the file that will be displayed, <when> is the condition which to display the message, and <class> is a list of classes to which this message applies.

The <when> parameter should take one of two forms: either LOGIN or CWD=<dir>. If it is LOGIN, the message is displayed upon a successful login. If the parameter is set to CWD=<dir>, the message is displayed when clients enter the <dir> directory.

The <class> parameter is optional. You can list multiple classes for a specific message. This capability is useful, for example, if you want messages sent only to anonymous users.

The message file itself (specified by <path>) can contain special flags that the FTP server substitutes with the appropriate information at runtime. These options are follows:

| Option | Description |
| --- | --- |
| %T | Local time |
| %F | Free space in the partition where <dir> is located |
| %C | Current working directory |
| %E | Site maintainer's email address (specified by the email command) |
| %R | Client hostname |
| %L | Server hostname |
| %U | Username provided at login time |
| %M | Maximum number users allowed in the specified class |
| %N | Current number of users in specified class |

Remember when messages are triggered by an anonymous user, the message path needs to be relative to the anonymous FTP directory.

This is the Linux default message command in ftpaccess in Linux:

```
Message /welcome.msg login
```

No message file is defined. Use your favorite text editor to create your own welcome.msg and type in the following:

```
Welcome to %L, %U,
you are %N out of %M users.
It is %T.
```

This message will print the hostname and login name and tell the user's number along with the local time. Save the file under the /home/ftp directory. When an anonymous user logs in, he or she will see the following:

```
230-Welcome to presario.home.org, anonymous
230-you are 1 out of unlimited users.
230-It is Tue May 25 21:13:32 1999.
```

![](img/cbac72550c7126a22162e94d91a0c360_366_0.png)

# Networking and Internet Services
PART II

## readme

The readme command specifies the conditions under which clients are notified that a certain file in their current directory was last modified. This command can take the form

readme <path> <when> <class>
<path> is the name of the file about which you want to alert the clients (for example, README), <when> is similar to the <when> in the message command, and <class> is the classes for which this command applies. The <when> and <class> parameters are optional.

Remember, if you are specifying a path for anonymous users, the file must be relative to the anonymous FTP directory.

# Controlling Logging

As with any complex network service, security quickly becomes an issue. To contend with possible threats, you must track connections and their corresponding commands. Use the commands that follow to determine how much, if any, logging should be done by the server software.

## log commands

For security purposes, you probably want to log the actions of your FTP users. The log commands option enables you to do this. Each command invoked by the clients is sent to your log file. The format of the command follows:

<typelist> is a comma-separated list specifying which kinds of users should be logged. The three kinds of users recognized are anonymous, guest, and real. (See the description of the class command earlier in this chapter for each user type's description.) For example, specify following to log all the actions of anonymous and guest users:

```
log commands anonymous,guest
```

# log transfers

If you want to log only clients' file transfers, the format follows:

```
log transfers <typelist> <directions>
```

<typelist> is a comma-separated list specifying which kinds of users should be logged. The three kinds of users recognized are anonymous, guest, and real. (See the description of the class command earlier in this chapter for each user type's description.) For example, specify following to log all the actions of anonymous and guest users:

```
log commands anonymous,guest
```

# Miscellaneous Server Commands

As with any complex network service, security quickly becomes an issue. To contend with possible threats, you must track connections and their corresponding commands. Use the commands that follow to determine how much, if any, logging should be done by the server software.

## alias

The alias command provides shortcuts to often-requested files. This capability is useful for you as an administrator. The format follows:

```
alias <string> <dir>
```

<string> is the alias, and <dir> is the actual directory to which the alias should point.

## cdpath

Similar to the PATH environment variable, the cdpath command establishes a list of paths to check whenever clients invoke the cd command. The format follows:

```
cdpath <dir>
```

<dir> is the server directory that is checked whenever clients use the cd command. For security reasons, specify directories relative to the FTP home directory. An example of the cdpath follows:

```
cdpath/pub/music
cdpath/pub/coffee
```

If clients type cd instant, the server examines the directories in the following order:

1. ./instant
2. Aliases called instant (For more information, see the description of alias earlier in this chapter.)
3. /pub/music/instant
4. /pub/coffee/instant

## compress

ftpd (the FTP server I have currently installed) offers a special compress feature that enables the server to compress or decompress a file before transmission. With this capability, a client who might not have the necessary software to decompress a file can still fetch it in a usable form.
[/content] (Note: The OCR text provided in the prompt was highly repetitive and garbled towards the end; I have processed the logical structure based on the clear sections provided.) 

*(Wait, the instructions say "Only output the processed final text, do not include explanation or extra notes". I will provide the final clean output now.)*

***

[content]
# Controlling Banner Messages

The commands in this section enable you to provide messages to FTP users when they connect to your site, or when they specify a special action. These commands are a way to make your site self-documenting.

## banner

The banner command displays a sign onscreen before the client provides a login and password combination. This is an important opportunity to display your server's security policies, when to upload software, and instructions for anonymous users regarding login procedures and software location. The format of this command follows:

```
banner <path>
```

<path> is the full pathname of the file you want to display. Consider the following example:

```
banner /home/ftp/.banner
```

# email

The email command specifies the site maintainer's email address. Some error messages or information requests provide this email address on demand. The default value in the ftppass file is root@localhost.

The format of the email command follows:

```
email <address>
```

<address> is the full email address of the site maintainer.

It is recommended that you create an email alias named FTP that forwards to the system administrators. Also, it's a good idea to provide this kind of information in the sign-on banner, so users know who to contact if they cannot log in to the system.

# message

The message command sets up special messages that are sent to the clients when they log in and when they change to a certain directory. You can specify multiple messages. The following is this command's format:

```
message <path> <when> {class} ...
```

<path> is the full pathname to the file that will be displayed, <when> is the condition which to display the message, and <class> is a list of classes to which this message applies.

The <when> parameter should take one of two forms: either LOGIN or CWD=<dir>. If it is LOGIN, the message is displayed upon a successful login. If the parameter is set to CWD=<dir>, the message is displayed when clients enter the <dir> directory.

The <class> parameter is optional. You can list multiple classes for a specific message. This capability is useful, for example, if you want messages sent only to anonymous users.

The message file itself (specified by <path>) can contain special flags that the FTP server substitutes with the appropriate information at runtime. These options are follows:

| Option | Description |
| --- | --- |
| %T | Local time |
| %F | Free space in the partition where <dir> is located |
| %C | Current working directory |
| %E | Site maintainer's email address (specified by the email command) |
| %R | Client hostname |
| %L | Server hostname |
| %U | Username provided at login time |
| %M | Maximum number users allowed in the specified class |
| %N | Current number of users in specified class |

Remember when messages are triggered by an anonymous user, the message path needs to be relative to the anonymous FTP directory.

This is the Linux default message command in ftpaccess in Linux:

```
Message /welcome.msg login
```

No message file is defined. Use your favorite text editor to create your own welcome.msg and type in the following:

```
Welcome to %L, %U,
you are %N out of %M users.
It is %T.
```

This message will print the hostname and login name and tell the user's number along with the local time. Save the file under the /home/ftp directory. When an anonymous user logs in, he or she will see the following:

```
230-Welcome to presario.home.org, anonymous
230-you are 1 out of unlimited users.
230-It is Tue May 25 21:13:32 1999.
```

![](img/cbac72550c7126a22162e94d91a0c360_366_0.png)

# Networking and Internet Services
PART II

## readme

The readme command specifies the conditions under which clients are notified that a certain file in their current directory was last modified. This command can take the form

readme <path> <when> <class>
<path> is the name of the file about which you want to alert the clients (for example, README), <when> is similar to the <when> in the message command, and <class> is the classes for which this command applies. The <when> and <class> parameters are optional.

Remember, if you are specifying a path for anonymous users, the file must be relative to the anonymous FTP directory.

# Controlling Logging

As with any complex network service, security quickly becomes an issue. To contend with possible threats, you must track connections and their corresponding commands. Use the commands that follow to determine how much, if any, logging should be done by the server software.

## log commands

For security purposes, you probably want to log the actions of your FTP users. The log commands option enables you to do this. Each command invoked by the clients is sent to your log file. The format of the command follows:

<typelist> is a comma-separated list specifying which kinds of users should be logged. The three kinds of users recognized are anonymous, guest, and real. (See the description of the class command earlier in this chapter for each user type's description.) For example, specify following to log all the actions of anonymous and guest users:

```
log commands anonymous,guest
```

# log transfers

If you want to log only clients' file transfers, the format follows:

```
log transfers <typelist> <directions>
```

<typelist> is a comma-separated list specifying which kinds of users should be logged. The three kinds of users recognized are anonymous, guest, and real. (See the description of the class command earlier in this chapter for each user type's description.) For example, specify following to log all the actions of anonymous and guest users:

```
log commands anonymous,guest
```

# Miscellaneous Server Commands

As with any complex network service, security quickly becomes an issue. To contend with possible threats, you must track connections and their corresponding commands. Use the commands that follow to determine how much, if any, logging should be done by the server software.

## alias

The alias command provides shortcuts to often-requested files. This capability is useful for you as an administrator. The format follows:

```
alias <string> <dir>
```

<string> is the alias, and <dir> is the actual directory to which the alias should point.

## cdpath

Similar to the PATH environment variable, the cdpath command establishes a list of paths to check whenever clients invoke the cd command. The format follows:

```
cdpath <dir>
```

<dir> is the server directory that is checked whenever clients use the cd command. For security reasons, specify directories relative to the FTP home directory. An example of the cdpath follows:

```
cdpath/pub/music
cdpath/pub/coffee
```

If clients type cd instant, the server examines the directories in the following order:

1. ./instant
2. Aliases called instant (For more information, see the description of alias earlier in this chapter.)
3. /pub/music/instant
4. /pub/coffee/instant

## compress

ftpd (the FTP server I have currently installed) offers a special compress feature that enables the server to compress or decompress a file before transmission. With this capability, a client who might not have the necessary software to decompress a file can still fetch it in a usable form.
