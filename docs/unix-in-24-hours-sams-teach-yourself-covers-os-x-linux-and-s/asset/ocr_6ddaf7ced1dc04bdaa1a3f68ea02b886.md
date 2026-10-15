# Note

One trick for using the ls command within sftp is that if you specify a set of command flags as a second word, it works fine as shown. Specify a third argument, however, and sftp saves the output of the command into a local file by that name; so ls -l -C would create a file called -C on your system with the output of the ls -l command. Awkward.

3. To transfer the file login.txt from the remote system, I can use the get command:

Click here to view code image

```
sftp> get login.txt
Fetching /home/taylor/login.txt to login.txt
100%  46    0.0KB/s   00:00
/home/taylor/login.txt
sftp>
```

This can get a bit tricky. I’ve just copied the login.txt file from intuitive.com (where I SFTP’d) to the local Unix system where I’m running the sftp command itself. On the local system, SFTP gave the file the same name as it had on the remote system: login.txt.

4. Alternatively, I could use get and specify a wildcard pattern similar to one I’d give the shell:

Click here to view code image

```
sftp> get log*
Fetching /home/taylor/login.txt to login.txt
/home/taylor/login.txt    100%   46    0.0KB/s   00:01    f
```

There was only one match, so the transfer was easy. The wildcard forms of get and put are particularly useful if you want to transfer many files at once, so get *.? would get *.c, *.h, and any other source files that have a single-letter suffix to their filenames, for example.

That job was easily accomplished. In the next task I will look on another system that supports anonymous FTP to see what’s available.

5. To disconnect, I enter quit:

```
sftp> quit
$
```

Though the interface is relatively crude, SFTP provides an easy and efficient method of transferring files quickly between two systems, regardless of operating system. It’s worth learning, but if you’d prefer, you can always get a nice graphical front end, either within X11, Windows, or the Mac environment.