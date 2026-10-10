where *filename* is the name of the file (with full path) that you want displayed. The file should be a straight ASCII text file. For example:

```
banner  /home/ftp/welcome_to_my_ftp_site
```

> **NOTE:**  Administrators who have taken care of busy FTP servers have commented that a good banner message is actually very crucial in limiting the number of one-user inquires about your site. To quote my technical editor, “People actually do read them!”

**EMAIL**  The *email* command allows you to specify the e-mail address of the site maintainer. Commands such as *message* (discussed later) use this information as well. The format of this command is

```
email *address*
```

where *address* is the e-mail address of the site administrator. You should consider using a generic e-mail address here such as “ftp@ftp.yoursite.com” and use the *etc/aliases* file (see Chapter 15 on Sendmail) to expand that alias to all of your real administrators. An example of the email command in action is

```
email ftp@ftp.yoursite.com
```

**MESSAGE**  The *message* command is useful when you need to set up special messages for a specific class of users or for users who enter a specific directory. The format of the command is

```
message *path* [*when* [*class*. . .]]
```

where *path* is the file that is to be displayed to the user, *when* is the condition that must be true in order for you to display the message, and *class* (which is optional) is the list of classes it applies to.

The *when* parameter is what makes this command really different from the *banner* command. *When* can take one of two forms, LOGIN or CWD=path. If it is LOGIN, the message is displayed after a successful login. If it is CWD=path, the *message* is displayed when a user goes into the *path* directory.

The *message* file itself is an ordinary text file with some special keywords. These keywords are as follows:

| Option | Description |
| %T | Local time |
| %F | Free space for the partition on which path is located |
| %C | The current working directory |
| %E | The e-mail address specified with the email command |