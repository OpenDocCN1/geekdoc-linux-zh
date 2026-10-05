
Users may be interested in the wget package. wget can download software using FTP or
HTTP with a single command line, such as the following:
get ftp://aptiva.home.org/home/bball/happy2.jpg

> Note
> SuSE users can use the SuSE ftp client to achieve the same effect for FTP servers:
> ftp://aptiva.home.org/home/bball/happy.jpg

Note that, although some of these utilities permit specifying passwords on the command
line, doing so can pose a security risk and is therefore not recommended.

Another ftp command feature is .netrc. You can use it to accomplish the same task as the
preceding command-line example. First, use your favorite text editor to create the file
.netrc in your home directory; then enter a series of auto-login lines similar to this:

```
machine aptiva.home.org
login bball
password mypassword
macdef init
get happy2.jpg
bye
```

> Caution
> The one disadvantage of .netrc is that passwords are left on the system in the
clear. This can present significant security risks. The file, .netrc should have
permissions to 600.

The first line in the file uses the machine keyword to specify a remote computer. The next
two lines specify your remote login and password. The macdef and init keywords
spec the start of an auto-executing macro. Any FTP commands placed following these
keywords and two blank lines are executed. In the previous example, the get command is
used to retrieve the file happy2.jpg, and the bye command is used to quit the connection.

Save the .netrc file and edit your editor. Next, use the chmod command to give the file
read and write permissions of 600:

```
# chmod 600 .netrc
```

# Networking and Internet Services
PART II

Finally, to test your .netrc file, use ftp with the hostname of the remote computer on the
command line:

+   # ftp aptiva
Connected to aptiva.home.org.
220 aptiva.home.org FTP server (Version wu-2.4.2-academ[BETA-18])(1)
Mon Aug 3 19:17:20 EDT 1998) ready.
331 Password required for bball
230 User bball logged in.
get happy2.jpg
local: happy2.jpg remote: happy2.jpg
227 Entering Passive Mode (192,168,26,35,0)
150 Opening ASCII mode connection for happy2.jpg (34636 bytes).
100% !******************************************* 34718 00:00 ETA
226 Transfer complete.
34718 bytes received in 0.05 seconds (698.5 KB/s)
221 Goodbye.

As you can see, the .netrc file connected, retrieved the file, and quit the
connection. You can use this approach to regularly retrieve files from remote computers
(such as web maps); to regularly upload files to remote sites (such as Web page
directories); or to automate other file transfer tasks (such as regular, remote transfers of
system logs using crontab entries).

# autoexpect

The tool-rich Linux environment features many different software tools (such as expect)
at you can use to accomplish difficult tasks. Another way to automate file transfers
(and other tasks) is with the autoexpect command. The autoexpect command (packaged
installed with the expect rpm) creates an expect script to accomplish tasks performed
during an autoexpect session.

To automate an FTP transfer, use the autoexpect command's -f command-line option,
followed by the name of the desired command, and an initial command line:

+   # expect -f ftp aptiva.home.org
autoexpect started, file is eftp
Connected to aptiva.home.org.
220 aptiva.home.org FTP server (Version wu-2.4.2-academ[BETA-18])(1)
Mon Aug 3 19:17:20 EDT 1998) ready.
Name (aptiva:): bball
ball
331 Password required for bball.

# FTP CHAPTER 10 351

Password:mypassword

```
230 User bball logged in.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> get happy2.jpg
get happy2.jpg
local: happy2.jpg remote: happy2.jpg
227 Entering Passive Mode (192,168,23,6,54)
150 Opening Binary mode data connection for happy2.jpg (34636 bytes).
100%
****************************************************
-! 34636 00:00 ETA
226 Transfer complete.
34636 bytes received in 0.03 seconds (1.10 MB/s)
ftp> bye
bye
221 Goodbye.
autexpect done, file is eftp
```

This session creates an executable file named eftp, which connects to the remote
computer, logs, retrieves the file happy2.jpg, and then disconnects. To perform the
automatic FTP session, type eftp on the command line:

```
# ./eftp
```

> Tip
> If the generated program works too fast, open the file (it is an expect command
> it is an expect command) and then disconnects.

# autoexpect

The tool-rich Linux environment features many different software tools (such as expect)
at you can use to accomplish difficult tasks. Another way to automate file transfers
(and other tasks) is with the autoexpect command. The autoexpect command (packaged
installed with the expect rpm) creates an expect script to accomplish tasks performed
during an autoexpect session.

To automate an FTP transfer, use the autoexpect command's -f command-line option,
followed by the name of the desired command, and an initial command line:

+   # expect -f ftp aptiva.home.org
autoexpect started, file is eftp
Connected to aptiva.home.org.
220 aptiva.home.org FTP server (Version wu-2.4.2-academ[BETA-18])(1)
Mon Aug 3 19:17:20 EDT 1998) ready.
Name (aptiva:): bball
ball
331 Password required for bball.

Password:mypassword

```
230 User bball logged in.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> get happy2.jpg
get happy2.jpg
local: happy2.jpg remote: happy2.jpg
227 Entering Passive Mode (192,168,23,6,54)
150 Opening Binary mode data connection for happy2.jpg (34636 bytes).
100%
****************************************************
-! 34636 00:00 ETA
226 Transfer complete.
34636 bytes received in 0.03 seconds (1.10 MB/s)
ftp> bye
bye
221 Goodbye.
autexpect done, file is eftp
```

This session creates an executable file named eftp, which connects to the remote
computer, logs, retrieves the file happy2.jpg, and then disconnects. To perform the
automatic FTP session, type eftp on the command line:

```
# ./eftp
```

> Tip
> If the generated program works too fast, open the file (it is an expect command
> it is an expect command) and then disconnects.

# autoexpect

The tool-rich Linux environment features many different software tools (such as expect)
at you can use to accomplish difficult tasks. Another way to automate file transfers
(and other tasks) is with the autoexpect command. The autoexpect command (packaged
installed with the expect rpm) creates an expect script to accomplish tasks performed
during an autoexpect session.

To automate an FTP transfer, use the autoexpect command's -f command-line option,
followed by the name of the desired command, and an initial command line:

+   # expect -f ftp aptiva.home.org
autoexpect started, file is eftp
Connected to aptiva.home.org.
220 aptiva.home.org FTP server (Version wu-2.4.2-academ[BETA-18])(1)
Mon Aug 3 19:17:20 EDT 1998) ready.
Name (aptiva:): bball
ball
331 Password required for bball.

Password:mypassword

```
230 User bball logged in.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> get happy2.jpg
get happy2.jpg
local: happy2.jpg remote: happy2.jpg
227 Entering Passive Mode (192,168,23,6,54)
150 Opening Binary mode data connection for happy2.jpg (34636 bytes).
100%
****************************************************
-! 34636 00:00 ETA
226 Transfer complete.
34636 bytes received in 0.03 seconds (1.10 MB/s)
ftp> bye
bye
221 Goodbye.
autexpect done, file is eftp
```

This session creates an executable file named eftp, which connects to the remote
computer, logs, retrieves the file happy2.jpg, and then disconnects. To perform the
automatic FTP session, type eftp on the command line:

```
# ./eftp
```

> Tip
> If the generated program works too fast, open the file (it is an expect command
> it is an expect command) and then disconnects.

# autoexpect

The tool-rich Linux environment features many different software tools (such as expect)
at you can use to accomplish difficult tasks. Another way to automate file transfers
(and other tasks) is with the autoexpect command. The autoexpect command (packaged
installed with the expect rpm) creates an expect script to accomplish tasks performed
during an autoexpect session.

To automate an FTP transfer, use the autoexpect command's -f command-line option,
followed by the name of the desired command, and an initial command line:

+   # expect -f ftp aptiva.home.org
autoexpect started, file is eftp
Connected to aptiva.home.org.
220 aptiva.home.org FTP server (Version wu-2.4.2-academ[BETA-18])(1)
Mon Aug 3 19:17:20 EDT 1998) ready.
Name (aptiva:): bball
ball
331 Password required for bball.

Password:mypassword

```
230 User bball logged in.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> get happy2.jpg
get happy2.jpg
local: happy2.jpg remote: happy2.jpg
227 Entering Passive Mode (192,168,23,6,54)
150 Opening Binary mode data connection for happy2.jpg (34636 bytes).
100%
****************************************************
-! 34636 00:00 ETA
226 Transfer complete.
34636 bytes received in 0.03 seconds (1.10 MB/s)
ftp> bye
bye
221 Goodbye.
autexpect done, file is eftp
```

This session creates an executable file named eftp, which connects to the remote
computer, logs, retrieves the file happy2.jpg, and then disconnects. To perform the
automatic FTP session, type eftp on the command line:

```
# ./eftp
```

> Tip
> If the generated program works too fast, open the file (it is an expect command
> it is an expect command) and then disconnects.

# autoexpect

The tool-rich Linux environment features many different software tools (such as expect)
at you can use to accomplish difficult tasks. Another way to automate file transfers
(and other tasks) is with the autoexpect command. The autoexpect command (packaged
installed with the expect rpm) creates an expect script to accomplish tasks performed
during an autoexpect session.

To automate an FTP transfer, use the autoexpect command's -f command-line option,
followed by the name of the desired command, and an initial command line:

+   # expect -f ftp aptiva.home.org
autoexpect started, file is eftp
Connected to aptiva.home.org.
220 aptiva.home.org FTP server (Version wu-2.4.2-academ[BETA-18])(1)
Mon Aug 3 19:17:20 EDT 1998) ready.
Name (aptiva:): bball
ball
331 Password required for bball.

Password:mypassword

```
230 User bball logged in.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> get happy2.jpg
get happy2.jpg
local: happy2.jpg remote: happy2.jpg
227 Entering Passive Mode (192,168,23,6,54)
150 Opening Binary mode data connection for happy2.jpg (34636 bytes).
100%
****************************************************
-! 34636 00:00 ETA
226 Transfer complete.
34636 bytes received in 0.03 seconds (1.10 MB/s)
ftp> bye
bye
221 Goodbye.
autexpect done, file is eftp
```

This session creates an executable file named eftp, which connects to the remote
computer, logs, retrieves the file happy2.jpg, and then disconnects. To perform the
automatic FTP session, type eftp on the command line:

```
# ./eftp
```

As you can see, the .netrc file connected, retrieved the file, and quit the
connection. You can use this approach to regularly retrieve files from remote computers
(such as web maps); to regularly upload files to remote sites (such as Web page
directories); or to automate other file transfer tasks (such as regular, remote transfers of
system logs using crontab entries).

# autoexpect

The tool-rich Linux environment features many different software tools (such as expect)
at you can use to accomplish difficult tasks. Another way to automate file transfers
(and other tasks) is with the autoexpect command. The autoexpect command (packaged
installed with the expect rpm) creates an expect script to accomplish tasks performed
during an autoexpect session.

To automate an FTP transfer, use the autoexpect command's -f command-line option,
followed by the name of the desired command, and an initial command line:

+   # expect -f ftp aptiva.home.org
autoexpect started, file is eftp
Connected to aptiva.home.org.
220 aptiva.home.org FTP server (Version wu-2.4.2-academ[BETA-18])(1)
Mon Aug 3 19:17:20 EDT 1998) ready.
Name (aptiva:): bball
ball
331 Password required for bball.

# FTP CHAPTER 10 351

Password:mypassword

```
230 User bball logged in.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> get happy2.jpg
get happy2.jpg
local: happy2.jpg remote: happy2.jpg
227 Entering Passive Mode (192,168,23,6,54)
150 Opening Binary mode data connection for happy2.jpg (34636 bytes).
100%
****************************************************
-! 34636 00:00 ETA
226 Transfer complete.
34636 bytes received in 0.03 seconds (1.10 MB/s)
ftp> bye
bye
221 Goodbye.
autexpect done, file is eftp
```

This session creates an executable file named eftp, which connects to the remote
computer, logs, retrieves the file happy2.jpg, and then disconnects. To perform the
automatic FTP session, type eftp on the command line:

```
# ./eftp
```

> Tip
> If the generated program works too fast, open the file (it is an expect command
> it is an expect command) and then disconnects.

# Networking and Internet Services
PART II

Finally, to test your .netrc file, use ftp with the hostname of the remote computer on the
command line:

+   # ftp aptiva
Connected to aptiva.home.org.
220 aptiva.home.org FTP server (Version wu-2.4.2-academ[BETA-18])(1)
Mon Aug 3 19:17:20 EDT 1998) ready.
331 Password required for bball
230 User bball logged in.
get happy2.jpg
local: happy2.jpg remote: happy2.jpg
227 Entering Passive Mode (192,168,26,35,0)
150 Opening ASCII mode connection for happy2.jpg (34636 bytes).
100% !******************************************* 34718 00:00 ETA
226 Transfer complete.
34718 bytes received in 0.05 seconds (698.5 KB/s)
221 Goodbye.

As you can see, the .netrc file connected, retrieved the file, and quit the
connection. You can use this approach to regularly retrieve files from remote computers
(such as web maps); to regularly upload files to remote sites (such as Web page
directories); or to automate other file transfer tasks (such as regular, remote transfers of
system logs using crontab entries).

# autoexpect

The tool-rich Linux environment features many different software tools (such as expect)
at you can use to accomplish difficult tasks. Another way to automate file transfers
(and other tasks) is with the autoexpect command. The autoexpect command (packaged
installed with the expect rpm) creates an expect script to accomplish tasks performed
during an autoexpect session.

To automate an FTP transfer, use the autoexpect command's -f command-line option,
followed by the name of the desired command, and an initial command line:

+   # expect -f ftp aptiva.home.org
autoexpect started, file is eftp
Connected to aptiva.home.org.
220 aptiva.home.org FTP server (Version wu-2.4.2-academ[BETA-18])(1)
Mon Aug 3 19:17:20 EDT 1998) ready.
Name (aptiva:): bball
ball
331 Password required for bball.

# FTP CHAPTER 10 351

Password:mypassword

```
230 User bball logged in.
Remote system type is UNIX.
Using binary mode to transfer files.
...
 (192,168,23,6,54)
150 Opening Binary mode data connection for happy2.jpg (34636 bytes).
100%
****************************************************
-! 34636 00:00 ETA
226 Transfer complete.
34636 bytes received in 0.03 seconds (1.10 MB/s)
ftp> bye
bye
221 Goodbye.
autexpect done, file is eftp
```

This session creates an executable file named eftp, which connects to the remote
computer, logs, retrieves the file happy2.jpg, and then disconnects. To perform the
automatic FTP session, type eftp on the command line:

```
# ./eftp
```

> Tip
> If the generated program works too fast, open the file (it is an expect command
> it is an expect command) and then disconnects.

# Networking and Internet Services
PART II

Finally, to test your .netrc file, use ftp with the hostname of the remote computer on the
command line:

+   # ftp aptiva
Connected to aptiva.home.org.
220 aptiva.home.org FTP server (Version wu-2.4.2-academ[BETA-18])(1)
Mon Aug 3 19:17:20 EDT 1998) ready.
331 Password required for bball
230 User bball logged in.
get happy2.jpg
local: happy2.jpg remote: happy2.jpg
227 Entering Passive Mode (192,168,26,35,0)
150 Opening ASCII mode connection for happy2.jpg (34636 bytes).
100% !******************************************* 34718 00:00 ETA
226 Transfer complete.
34718 bytes received in 0.05 seconds (698.5 KB/s)
221 Goodbye.

As you can see, the .netrc file connected, retrieved the file, and quit the
connection. You can use this approach to regularly retrieve files from remote computers
(such as web maps); to regularly upload files to remote sites (such as Web page
directories); or to automate other file transfer tasks (such as regular, remote transfers of
system logs using crontab entries).

# autoexpect

The tool-rich Linux environment features many different software tools (such as expect)
at you can use to accomplish difficult tasks. Another way to automate file transfers
(and other tasks) is with the autoexpect command. The autoexpect command (packaged
installed with the expect rpm) creates an expect script to accomplish tasks performed
during an autoexpect session.

To automate an FTP transfer, use the autoexpect command's -f command-line option,
followed by the name of the desired command, and an initial command line:

+   # expect -f ftp aptiva.home.org
autoexpect started, file is eftp
Connected to aptiva.home.org.
220 aptiva.home.org FTP server (Version wu-2.4.2-academ[BETA-18])(1)
Mon Aug 3 19:17:20 EDT 1998) ready.
Name (aptiva:): bball
ball
331 Password required for bball.

# FTP CHAPTER 10 351

Password:mypassword

```
230 User bball logged in.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> get happy2.jpg
get happy2.jpg
local: happy2.jpg remote: happy2.jpg
227 Entering Passive Mode (192,168,23,6,54)
150 Opening Binary mode data connection for happy2.jpg (34636 bytes).
100%
****************************************************
-! 34636 00:00 ETA
226 Transfer complete.
34636 bytes received in 0.03 seconds (1.10 MB/s)
ftp> bye
bye
221 Goodbye.
autexpect done, file is eftp
```

This session creates an executable file named eftp, which connects to the remote
computer, logs, retrieves the file happy2.jpg, and then disconnects. To perform the
automatic FTP session, type eftp on the command line:

```
# ./eftp
```

> Tip
> If the generated program works too fast, open the file (it is an expect command
> it is an expect command) and then disconnects.

# autoexpect

The tool-rich Linux environment features many different software tools (such as expect)
at you can use to accomplish difficult tasks. Another way to automate file transfers
(and other tasks) is with the autoexpect command. The autoexpect command (packaged
installed with the expect rpm) creates an expect script to accomplish tasks performed
during an autoexpect session.

To automate an FTP transfer, use the autoexpect command's -f command-line option,
followed by the name of the desired command, and an initial command line:

+   # expect -f ftp aptiva.home.org
autoexpect started, file is eftp
Connected to aptiva.home.org.
220 aptiva.home.org FTP server (Version wu-2.4.2-academ[BETA-18])(1)
Mon Aug 3 19:17:20 EDT 1998) ready.
Name (aptiva:): bball
ball
331 Password required for bball.

Password:mypassword

```
230 User bball logged in.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> get happy2.jpg
get happy2.jpg
local: happy2.jpg remote: happy2.jpg
227 Entering Passive Mode (192,168,23,6,54)
150 Opening Binary mode data connection for happy2.jpg (34636 bytes).
100%
****************************************************
-! 34636 00:00 ETA
226 Transfer complete.
34636 bytes received in 0.03 seconds (1.10 MB/s)
ftp> bye
bye
221 Goodbye.
autexpect done, file is eftp
```

This session creates an executable file named eftp, which connects to the remote
computer, logs, retrieves the file happy2.jpg, and then disconnects. To perform the
automatic FTP session, type eftp on the command line:

```
# ./eftp
```

> Tip
> If the generated program works too fast, open the file (it is an expect command
> it is an expect command) and then disconnects.

# autoexpect

The tool-rich Linux environment features many different software tools (such as expect)
at you can use to accomplish difficult tasks. Another way to automate file transfers
(and other tasks) is with the autoexpect command. The autoexpect command (packaged
installed with the expect rpm) creates an expect script to accomplish tasks performed
during an autoexpect session.

To automate an FTP transfer, use the autoexpect command's -f command-line option,
followed by the name of the desired command, and an initial command line:

+   # expect -f ftp aptiva.home.org
autoexpect started, file is eftp
Connected to aptiva.home.org.
220 aptiva.home.org FTP server (Version wu-2.4.2-academ[BETA-18])(1)
Mon Aug 3 19:17:20 EDT 1998) ready.
Name (aptiva:): bball
ball
331 Password required for bball.

Password:mypassword

```
230 User bball logged in.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> get happy2.jpg
get happy2.jpg
local: happy2.jpg remote: happy2.jpg
227 Entering Passive Mode (192,168,23,6,54)
150 Opening Binary mode data connection for happy2.jpg (34636 bytes).
100%
****************************************************
-! 34636 00:00 ETA
226 Transfer complete.
34636 bytes received in 0.03 seconds (1.10 MB/s)
ftp> bye
bye
221 Goodbye.
autexpect done, file is eftp
```
