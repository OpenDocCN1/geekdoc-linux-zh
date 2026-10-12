```
restore > ls
./joe:
.netscape/ Desktop/ report.html
.tcshrc \*Mail/ letter.txt
.xinitrc News/ www/
```

Now use the extract command to begin the extraction process. restore will prompt you for the number of the tape to start with. This is a single tape backup, so just enter the number 1. When it prompts you to “set owner/mode for ‘. ’? ” answer yes by typing y and pressing Enter. restore will then set restore the file permissions (if necessary) of the directory it is restoring to. This isn’t critical when extracting individual files like this, but you should always answer yes to this prompt when doing a full restore. Anyway, your screen should now contain the following:

```
restore > extract
You have not read any tapes yet.
Unless you know which volume your file(s) are on you
should start with the last volume and work toward
the first.
Specify next volume #: 1
set owner/mode for ‘. ’? [yn] y
restore >
```

At this point, the files have been recovered and you can exit the restore program by issuing the quit command. That’s all there is to it. You now know the basics of using the dump and restore commands.

# Backing Up Over the Network

Using dump as described earlier works great when you have a tape drive physically connected to the system that you are backing up. But installing backup hardware in every single device on your network is hardly cost effective. Fortunately, dump has the capability to send data over the network to be written to a device on another server.

To direct the output of dump to a server on the network, you need to modify the backup device argument supplied with the -f option. Include the host name followed by a colon (:) character before the name of the backup device. The dump command will then look for that device on the remote system. For example, to make a backup of the /dev/hda7 partition but write it to a tape drive connected to the computer named ratbert, type the following:

```
# dump 0uBf 500000 ratbert:/dev/nrf0 /dev/hda7
```

Similarly, the restore command can also access devices connected to remote systems. Thus to restore the dump you just made, you would type:

```
# restore rf ratbert:/dev/nrft0
```