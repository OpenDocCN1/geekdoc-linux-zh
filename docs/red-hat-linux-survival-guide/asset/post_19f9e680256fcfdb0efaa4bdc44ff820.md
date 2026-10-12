
The preceding class definition allows real users to log on from any machine in the evoknow.com and ad-engine.com domains.

![](img/9eb7e89292d2f85707b4d49102c865b7_427_0.png)

If you are not planning on allowing anonymous or guest accounts on your FTP server, you can remove the “guest” and “anonymous” keywords from the default typelist for the all class.

## deny
This keyword is used to deny FTP service to hosts that match the IP addresses or domain names specified.

Syntax: deny addrglob message_file

For example, the following instruction tells the FTP server to deny access to anyone trying to access the server from a U.S. university:

```
deny *.edu
```

Here is another example:

```
deny *.com /etc/goaway.msg
```

This configuration denies FTP access to anyone in a .com domain and also displays the /etc/goaway.msg file.

## limit
This keyword limits the number of simultaneous user logins for the named class.

Syntax: limit class n times message_file

The arguments for limit are as follows:

- n is the number of users allowed access.
- times is when the limit should apply. The time can be specified in a 24-hour clock format. For example, 0700–1700 is a range that covers 7 a.m. to 5 p.m. The time format can also include days, as shown in Table 14-1.

## Table 14-1 The Time Format for limit

| Keyword | What It Means |
|---|---|
| Any | Any time |
| Wk | Any weekday |
| Sa | Saturday |
| Su | Sunday |
| Mo | Monday |
| Tu | Tuesday |
| We | Wednesday |
| Th | Thursday |
| Fr | Friday |

You can combine the days as well. For example, SaSu07–17 covers the weekend from 7 a.m. to 5 p.m. Here is an example configuration that sets limits on access:

```
class  local  real      *.evoknow.com
class  remote anonymous  *
```

```
limit local  200 Any /etc/msgs/msg.toomany
limit remote 100 Any /etc/msgs/msg.toomany
```

The preceding configuration allows up to 200 users from the evoknow.com domain to log on at any time. At the same time it allows only 100 anonymous users to access the system at any time.

## noretrieve
This keyword denies FTP users the ability to retrieve named files.

Syntax: noretrieve filename filename ...

For example, the following line denies anyone the ability to retrieve the /etc/passwd file:

```
noretrieve /etc/passwd
```

A message such as /etc/passwd is marked unretrievable is displayed. Note that if the filename does not include a fully qualified path name, all files with such names are marked unretrievable. For example, the following line prevents anyone from retrieving any file named passwd or core from any directory:

```
noretrieve passwd core
```

Note that you cannot use wildcards in the filename.

## loginfails
This keyword defines the number of times a user can attempt to log on before getting disconnected. When a user fails to enter a valid username/password pair for a login for the specified number of times, an error message is logged and the user is disconnected.

```
Syntax: loginfails number
```

```
Default: loginfails 5
```

## private
The wu-ftpd server provides an extended set of FTP commands that are nonstandard. One of these commands is called SITE. This command is considered a security risk, and therefore use of the private keyword is also not recommended. In fact, the SITE command is disabled in the default version of wu-ftpd that ships with Red Hat Linux. You have to compile wu-ftpd yourself to enable SITE, which is not recommended.

```
Syntax: private yes_or_no
```

## guestgroup
This keyword specifies the user groups that are to be considered as guest user accounts. See the section “Creating a guest FTP account” in this chapter for more details.

```
Syntax: guestgroup groupname groupname ...
```

## autogroup
This keyword enables you to change the effective group ID for an anonymous user if she belongs to one or more classes specified.

```
Syntax: autogroup groupname class [class ...]
```

## Informational configuration
You can specify an informational configuration using the banner, email, message, and readme keywords.

### banner
You can use this keyword to display the contents of the specified file. Typically, many systems use banners to identify the systems and also to provide user policy and contact information.

```
Syntax: banner filename
```

![](img/9eb7e89292d2f85707b4d49102c865b7_430_0.png)

> If you use the banner keyword to display a file before login, some nonstandard FTP clients may fail to log on, because they are unable to handle multiline responses from the server.

### email
This directive sets the e-mail address of the FTP site administrator.

```
Syntax: email user@host
```

```
Default: email root@localhost
```

### message
Use this keyword to set the name of a file to display when the user logs into the system or uses the change directory command to change directories.

```
Syntax: message path {when {class ...}}
```

```
Default: message /welcome.msg login
```

```
message .message cwd=*
```

For example, the first default setting in the preceding code displays the contents of the /welcome.msg file at successful user login. The second default setting shows the contents of the .message file whenever the user changes a directory. Nothing displays when the file to be displayed is missing.

The file to be displayed can contain one or more of the magic cookie strings shown in Table 14-2.

## Table 14-2 Magic Cookie Strings for Message Files

| Cookies | Replacement Text |
|---|---|
| %C | The current working directory |
| %E | The maintainer's e-mail address, as defined in ftpaccess |
| %F | Free space in partition of CWD (kilobytes) |
| %L | The local hostname |
| %M | The maximum number of users allowed in this class |
| %N | The current number of users in this class |
| %R | The remote hostname |
| %T | The local time (in the form "Thu Nov 15 17:12:42 2000") |
| %u | The username as determined via RFC 931 authentication |
| %U | The username given at login time |

Listing 14-2 shows the /welcome.msg file I use for my Red Hat Linux system.

## Listing 14-2 An example /welcome.msg file

```
Hello %U

Welcome to %L. You are user %N of possible %M users.
You are logging in from %R.

Local time is %T

Feel free to email (%E) if you have
any questions or comments.

Your current directory is %C (Free %F KB)
```

![](img/9eb7e89292d2f85707b4d49102c865b7_431_0.png)

The message file is displayed only once per directory. Also, if you plan to display message files for anonymous access, use relative paths to the base of the anonymous FTP directory tree.

### readme
This keyword is similar to the message keyword discussed previously. However, instead of displaying the contents of the named file, it makes the FTP server notify the user about the existence of the file and also tells the user about the modification date and time of the file.

```
Syntax: readme path {when {class ...} }
```

```
Default: readme README* login
readme README* cwd=*
```

## Logging configuration
You can specify a logging configuration using the log commands and log transfers keywords.

### log commands
This keyword enables you to log FTP commands for one or more types of users.

```
Syntax: log commands typelist
```

For example, the following directive logs all the FTP commands performed by all anonymous users:

```
log commands anonymous
```

### log transfers
This keyword enables you to log file transfers to and from the system. The default setting makes the server log both inbound and outbound file transfers for anonymous and real users.

```
Syntax: log transfers typelist directions
```

```
Default: log transfers anonymous,real inbound,outbound
```

## Permission configuration
The following keywords enable you to control file/directory permission settings for users.

### chmod
This keyword enables or disables the chmod command (site chmod) for user types specified in the list. For example, the default setting disables this command for both guest and anonymous users.
