
### su
Syntax: su [-] [username]

You can use the su command to change into another user. For example:

```
su john
```

This command allows you to be the user john as long as you know john's password, and this account exists on the server you use.

The most common use of this command is to become root. For example, if you run this command without any username argument, it assumes that you want to be root and prompts you for the root password. If you enter the correct root password, su runs a shell by using the root's UID (0) and GID (0). This allows you effectively to become the root user and to perform administrative tasks.

![](img/9eb7e89292d2f85707b4d49102c865b7_589_0.png)

This command is very useful if you have only Telnet access to the server. You can telnet into the server as a regular user and use it to become root to perform system administrative tasks. If you supply the – option, the new shell is marked as the login shell. Once you become the root user, you can su to other users without entering any password.

### useradd
See the section on creating new user accounts in Chapter 7.

### userdel
See the section on deleting or disabling a user account in Chapter 7.

### usermod
See the section on modifying an existing user account in Chapter 7.

### who
Syntax: who

This command displays information about the users who are currently logged into a system. You can also use the w command for the same purpose.

### whoami
Syntax: whoami

This command displays your current username.

## User Commands for Accessing Network Services
The commands that I discuss in this section allow you to access various network services. You can use these tools to get finger information on a user, transfer files, browse Web pages, read and send e-mails, Telnet to other systems, and so on.

### finger
Syntax: finger user@host

This program allows you to query a finger daemon at the named host. For example, the following command requests a finger connection to the finger daemon running on the blackhole.integrationlogic.com server:

```
finger kabir@blackhole.integrationlogic.com
```

If the named host does not allow finger connections, this attempt fails. On success, the finger request displays information about the named user. If the user has a .plan file in the home directory, most traditional finger daemons display this file. Because finger has been used by hackers to cause security problems, most system administrators disable finger service outside their domains.

### ftp
Syntax: ftp hostname or IP address

This is the default FTP client program. You can use this to FTP to an FTP server. For example:

```
ftp ftp.cdrom.com
```

This opens an FTP connection to ftp.cdrom.com and prompts you to enter a username and a password. If you know the username and password, you can log into the FTP server and upload or download files. Once you're at the FTP prompt, you can enter help or ? to get help on FTP commands.

### lynx
Syntax: lynx [-dump] [-head] [URL]

This is the most popular interactive text-based Web browser. For example, the following command displays the top page of the site:

```
lynx http://www.integrationlogic.com/
```

This is a very handy program to have. For example, say you want quickly to find what kind of Web server the site uses without asking the Webmaster. You can run the following command:

```
lynx -head http://www.integrationlogic.com/
```

This displays the HTTP header the lynx browser receives from the Web server. An example of output is shown here:

```
HTTP/1.1 302 Moved
Date: Tue, 02 Mar 1999 06:47:27 GMT
Server: Apache/1.3.3 (Unix)
Location: http://www.integrationlogic.com/index.shtml
Connection: close
Content-Type: text/html
```

As you can see, this header shows that www.integrationlogic.com runs on the Apache 1.3.3 Web server on a Unix platform. Note that not all Web sites give their Web server platform information, but most do. If you would like to avoid the interactive mode, you can use the -dump option to dump the page on the screen. For example,

```
lynx -dump -head http://www.integrationlogic.com/
```

This dumps the header to the screen. The -dump feature can be quite handy. For example:

```
lynx -dump -head http://webserver/new.gif > new.gif
```

This allows you to save new.gif on the Web server host on a local file called new.gif.

The interactive mode (i.e., without -dump) allows you to browse a text browser-friendly site in a reasonably nice manner.

### mail
**Syntax:** `mail user@host [-s subject] [< filename]`

This is the default SMTP mail client program. You can use this program to send or receive mail from your system. For example, if you run this program without any argument, it displays an & prompt and shows you the currently unread mail messages by listing them in a numeric list. To read a message, enter the index number and the mail is displayed. To learn more about mail, use the ? command once you are at the & prompt.

For example, to send a message to a user called kabir@evoknow.com with the subject header “About your Red Hat book,” you can run:

```
mail kabir@evoknow.com -s "About your Red Hat book"
```

You can then enter your mail message and press Ctrl+D to end the message. You can switch to your default text editor by entering ~v at the beginning of a line while you are in the compose mode. If you have already prepared a mail message in a file, you can send it using a command such as:

```
mail kabir@evoknow.com -s "About your Red Hat book" <<
feedback.txt
```

This sends a message with the given subject line; the message consists of the contents of the feedback.txt file.

### pine
Syntax: pine

This is a full-screen SMTP mail client that is quite user-friendly. If you typically use mail clients via telnet, you should definitely try this program. Because of its user-friendly interfaces, it is suitable for your Linux users who are not yet friends with Linux.

### rlogin
Syntax: rlogin [-l username] host

This command allows you to log remotely into a host. For example, to log into a host called shell.myhost.com, you can run:

```
rlogin shell.myhost.com
```

The -l option allows you to specify a username to use for authentication. If you would like to log remotely into a host without entering a password, create a .rhosts file in the user's home directory. Add the host name or IP address of the computer you use to issue the rlogin request.

![](img/9eb7e89292d2f85707b4d49102c865b7_593_0.png)

Because rlogin is not safe, I recommend that you use it only in a closed LAN environment.

### talk
Syntax: talk username [tty]

If you need to send a message to another user, e-mail works just fine. But if you need to communicate with another user in real-time, like a telephone conversation, use the talk command.

To talk to another user who is logged in, use the following command:

```
talk ronak@csus.edu
```

The user you request has to accept your talk request. Once the user accepts your talk request, you can begin talking (or typing) to each other. The talk program terminates when either party presses Ctrl+C (the program interrupt key combination). Also, note that if the user is logged in multiple times you have to specify the tty device name to talk to a specific instances of the user login. You can run w or who command to find the tty names for each user login.

### telnet
Syntax: `telnet hostname_or_IP_address [port]`

This is the default Telnet client program. You can use this program to connect to a Telnet server. For example:

```
telnet shell.myportal.com
```

This command opens a Telnet connection to the shell.myportal.com system if the named host runs a Telnet server. Once a connection is opened, the command prompts you for a username and password and, on successful login, allows you to access a local user account on the Telnet server.

### wall
Syntax: `wall`

This command allows you to send a text message to everyone’s terminal as long as he or she has not disabled write access to the tty via the mesg n command. After you type wall, you can enter a single or multiline message and can send it by pressing Ctrl+D.

## Network Administrator’s Commands
The commands that I discuss in this section allow you to gather information on network services and on the network itself. Using these commands you can get a host name by IP, display or set host name of the system you are on, configure network interfaces, perform network queries, and so on.
