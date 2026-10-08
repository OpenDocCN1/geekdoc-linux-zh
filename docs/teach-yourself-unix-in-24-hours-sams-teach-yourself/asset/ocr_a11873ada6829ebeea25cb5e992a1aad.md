you're an authorized person, and you want to have a directory on the top level, please contact Erik Fair <ftp@apple.com>, (408) 974-1779,
 explain why you want one, and what you're going to use it for.
Otherwise, make sure your staff available in the “public” directory.

There are no writeable directories for anonymous FTP on this server; it cannot be used as a drop box.

+   228 Transfer complete:
tlocal: [more remote]: README
433 bytes received in 0.21 seconds (2.01 Kbytes/s)
ftp>

8. There's a new Macintosh application on this system in dts/mac/hacks I've been interested in seeing. I can move directly there with cd, confirming that I'm here with I am with:

```
ftp cd dts/mac/hacks
250 command successful.
257 ".../mac/hacks" is current directory.
ls -CF
200 PORT command successful.
150 Opening ASCII mode connection for /bin/ls.
aertotracker-3-0.hqx mountains-1-0.hqx
application-2-1.hqx newsswatcher.hqx
appmenu-3-5.hqx okey-dey-1-0-1.hqx
bifon-flex.hqx piston.
colorfinder.hqx Oscar.hqx
darkside-of-the-mac-4-1.hqx snake.hqx
dropper.hqx switch-1-1.hqx
escape-damit-0-4.hqx system-1-1.hqx
extension-manager-2-0-1.hqx thread-manager-picker-1-0-2.hqx\lipper.hqx trashman-4-0-2.hqx
folder-maker-1-1.hqx understudy.hqx
fsid.hqx unlock_folder.hqx
in-mac-0-026w.hqx virtual-controllers.hqx
lockdisk-1-0.hqx xferit-1-4.hqx
```

+   226 Transfer complete.
-CF
559 bytes received in 0.14 seconds (3 Kbytes/s)
ftp>

Notice that there's an asterisk following the names of these files. This indicates, you know from the -F flag to ls that it is a binary file. I need to specify to ftp that it should transfer the file in binary mode, by entering binary:

```
ftp binary
200 Type set to I.
ftp>
```

I check to see how the big file is, then I can use get to transfer it and drop the connection by:

```
ftp dir colorfinder.hqx
200 PORT command successful.
150 Opening ASCII mode connection for /bin/ls.
```