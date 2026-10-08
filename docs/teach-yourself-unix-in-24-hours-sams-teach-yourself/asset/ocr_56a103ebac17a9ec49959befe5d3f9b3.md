# Using telnet and ftp 487

There was only one match, so the transfer was easy. Entering anything other than that at the `get login?` prompt would have resulted in the file not being transferred.
That was easily accomplished. Now I will look on another system in the anonymous FTP directory to disconnect, see what's available.

+   5. To disconnect, I enter close so that I don't leave the ftp program:

```
ftp> close
221 Goodbye
ftp>
```

There are hundreds of information servers on the Internet, offering an astounding variety of information, from weather maps to the full text of the Bible and Alice in Wonderland to the source lists of thousands of different programs.

In this example, I want to look at the anonymous FTP archive at the Massachusetts Institute of Technology's Artificial Intelligence Laboratory. The host is called `ai.mit.edu`:

```
ftp> open ftp.ai.mit.edu
Connected to mini-wheats.ai.mit.edu.
220 mini-wheats FTP server (Version 2.1b Wed Aug 25 09:20 1993)
```

```
Name (ftp.ai.mit.edu:taylor): ftp
331 Guest login ok, send your complete e-mail address as password.
Password:
230-
```

```
230-Welcome to the MIT Artificial Intelligence Laboratory. If you are
230-interested in Artificial Intelligence Laboratory publications please
230-ftp to publications.ai.mit.edu.
230-
230-
230-
230 Guest login ok, access restrictions apply.
ftp>
```

Now I can use -CF to look around:

```
ftp> -CF
200 PORT command successful.
150 Opening ASCII mode data connection for /bin/ls.
.message bin/ etc/ pub/
ai-pubs/ dev/ incoming/ usr/
226 Transfer complete.
remote: -CF
58 bytes received in 0.39 seconds (0.15 Kbytes/s)
ftp>
```

It looks like there might be something of interest in the pub directory by this name usually contains public information. I used cd to change to the directory, then I ls -CF to see what's available there:

```
ftp> cd pub
250 CWD command successful.
ftp> ls -CF
```

![](bbox=[0.868, 0.246, 0.999, 0.335])