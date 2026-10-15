# NOTE

Note that the banner does not replace the greeting text that, by default, displays the hostname and server information, such as:

220 shuttle2 FTP server (Version wu-2.6.2-8) ready.

To hide version information, use the greeting command in ftpassess with a keyword, such as terse, like so:

```
greeting terse
```

FTP users then see a short message like this as part of the login text:

220 FTP server ready.

Also, not all FTP clients can handle multiline responses from the FTP server. The banner <path> command is how the banner line passes the file contents to the client. If clients cannot interrupt multiline responses, the FTP server is useless to them. You should also edit the default banner to remove identity and version information.

# Display a File

This line specifies a text file to be displayed to the user during login and when the user issues the cd command:

```
message <path> [{<when>} {<class> ...}]
```

The optional when clause can be LOGIN or CWD=(dir), where dir is the name of a directory that is current. The optional class parameter enables messages to be shown to only a given class or classes of users.

Using messages is a good way to give information about where things are on your site as well as information that is system dependent, such as alternative sites, general policies regarding available data, server availability times, and so on.

You can use magic cookies to breathe life into your displayed messages. Magic cookies are symbolic constants that are replaced by system information. Table 18.1 lists the message command's valid magic cookies and their representations.

# TABLE 18.1 Magic Cookies and Their Descriptions

| Cookie | Description |
| --- | --- |
| %T | Local time (form Thu Nov 15 17:12:42 1990) |
| %F | Free space in partition of CWD (kilobytes) |
| %C | [Not supported on all systems] |
| %C | Current working directory |
| %E | Maintainer's email address as defined in ftpassess |
| %R | Remote hostname |