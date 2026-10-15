
in front of it. You can use this command to assign permissions to a range of group IDs, as in this example:

```
guestgroup $500-$550
```

This entry restricts all users with the group IDs 500–550 to being treated as a guest group, rather than individual users. For guestgroup to work, you must set up the user's home directories with the correct permissions, exactly like the anonymous FTP user.

## Limit Permissions Based on Individual ID

The guestuser line works exactly like the guestgroup command you just read about, except it specifies a User ID (UID) instead of a group ID. Here's the command:

```
guestuser <username> | <username>
```

This command limits the guest user to files for which the user has privileges. Generally, a user has more privileges than a group, so this type of assignment can be less restrictive than the guestgroup line.

## Restrict the Number of Users in a Class

The limit command restricts the number of users in a class during given times. Here is the command, which contains fields for specifying a class, a number of users, a time range, and the name of a text file that contains an appropriate message:

```
limit <class> <n> <times> <message file>
```

If the specified number of users from the listed class is exceeded during the given time period, the user sees the contents of the file given in the message_file parameter.

The times parameter is somewhat terse. Its format is a comma-delimited string in the form of days, hours. Valid day strings are Su, Mo, Tu, We, Th, Fr, Sa, and Any. The hours are formatted in a 24-hour format. An example is as follows:

```
limit anonymous 10 MoTuWeThFr,Sa0000-2300 /home/ftp/.message_limit_anon_class
```

This line limits the anonymous class to 10 concurrent connections on Monday through Friday, and on Saturday from midnight to 11:00 p.m. If the number of concurrent connections is exceeded at or 11:00 p.m. on Saturday, the users will see the contents of the file /home/ftp/.message_limit_anon_class.

Syntax for finer control over limiting user connections can be found in the ftpdaccess man page.

## Limit the Number of Invalid Password Entries

This line allows control over how many times a user can enter an invalid password before the FTP server terminates the session:

```
loginfails <number>
```

## NOTE

Note that the banner does not replace the greeting text that, by default, displays the hostname and server information, such as:

220 shuttle2 FTP server (Version wu-2.6.2-8) ready.

To hide version information, use the greeting command in ftpdaccess with a keyword, such as terse, like so:

```
greeting terse
```

FTP users then see a short message like this as part of the login text:

220 FTP server ready.

Also, not all FTP clients can handle multiline responses from the FTP server. The banner <path> command is how the banner line passes the file contents to the client. If clients cannot interrupt multiline responses, the FTP server is useless to them. You should also edit the default banner to remove identity and version information.

## Display a File

This line specifies a text file to be displayed to the user during login and when the user issues the cd command:

```
message <path> [{<when>} {<class> ...}]
```

The optional when clause can be LOGIN or CWD=(dir), where dir is the name of a directory that is current. The optional class parameter enables messages to be shown to only a given class or classes of users.

Using messages is a good way to give information about where things are on your site as well as information that is system dependent, such as alternative sites, general policies regarding available data, server availability times, and so on.

You can use magic cookies to breathe life into your displayed messages. Magic cookies are symbolic constants that are replaced by system information. Table 18.1 lists the message command's valid magic cookies and their representations.

### TABLE 18.1 Magic Cookies and Their Descriptions

| Cookie | Description |
| --- | --- |
| %T | Local time (form Thu Nov 15 17:12:42 1990) |
| %F | Free space in partition of CWD (kilobytes) |
| %C | [Not supported on all systems] |
| %C | Current working directory |
| %E | Maintainer's email address as defined in ftpdaccess |
| %R | Remote hostname |
