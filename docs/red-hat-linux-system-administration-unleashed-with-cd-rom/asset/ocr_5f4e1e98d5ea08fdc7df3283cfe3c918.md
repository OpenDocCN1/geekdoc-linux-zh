```
set owner/mode for '.'? [yn] n
restore > quit
[root@clarence /root]# ls ./etc
cron.daily
[root@clarence /root]# ls ./etc/cron.daily/
logrotate
```

This particular implementation of restore dumps core if I just give the command add etc/cron.daily/logrotate without adding the cron.daily subdirectory first. I'm not exactly sure why, but since I have the source code, I could look through it and fix that particular bug. Or I could email the author a bug report. Or I could do what you see here, and work around it. The restore listing of the etc/cron.daily subdirectory has an asterisk in front of the name logrotate to indicate that it has been added to the extraction list. You will notice that the extraction restored the intervening etc/ subdirectory relative to my current working directory. This allows me to restore system files that may be broken now, because of upgrades, and just copy over what I want. The line about "specify next volume." comes in handy if the dump occupies several tapes and you know where the specific file you want is located.

# Quick Archiving with cpio

Another candidate for quick archiving is the cpio program, especially if you need to move from one kind of machine to another. The fact that cpio's default is to not create directories or overwrite existing files is either good or bad, depending on your needs of the moment.

There are many variations possible; consult the man and info pages for dump, find, tar, and cpio (info dump, info tar, info find, info cpio, man tar, man find, man cpio) to see some more examples.

Any of these commands can be placed into a script file and executed via cron. It is always a really good idea to run the script from the command line first, so that you can see if there are any errors in the output before you just let it go. If your script generates output on STDOUT (that's system administrator-speak for "The script has an echo line in it somewhere") the owner of the cron job will be mailed what would have been printed to the screen—perhaps a final line reading something along the lines of:

```
echo The backup script completed on `date`.
```

so that you will know it is time to replace the tape.