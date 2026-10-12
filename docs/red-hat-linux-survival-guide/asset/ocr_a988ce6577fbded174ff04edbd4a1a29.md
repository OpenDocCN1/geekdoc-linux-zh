# Informational configuration

You can specify an informational configuration using the banner, email, message, and readme keywords.

**banner** You can use this keyword to display the contents of the specified file. Typically, many systems use banners to identify the systems and also to provide user policy and contact information.

```
Syntax: banner filename
```

![](bbox=[0.07, 0.34, 0.18, 0.44])

> If you use the banner keyword to display a file before login, some nonstandard FTP clients may fail to log on, because they are unable to handle multiline responses from the server.

**email** This directive sets the e-mail address of the FTP site administrator.

```
Syntax: email user@host
```

```
Default: email root@localhost
```

**message** Use this keyword to set the name of a file to display when the user logs into the system or uses the change directory command to change directories.

```
Syntax: message path {when {class . . .}}
```

```
Default: message /welcome.msg login
```

```
message .message cwd=*
```

For example, the first default setting in the preceding code displays the contents of the /welcome.msg file at successful user login. The second default setting shows the contents of the .message file whenever the user changes a directory. Nothing displays when the file to be displayed is missing.

The file to be displayed can contain one or more of the magic cookie strings shown in Table 14-2.