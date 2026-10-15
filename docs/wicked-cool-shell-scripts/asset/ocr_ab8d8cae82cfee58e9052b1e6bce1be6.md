Done. remotebackup backed up the following files:
 ourecopass
 and mailed them to taylor@intuitive.com with requested target directory mirror

Listing 10-8: Running the remotebackup script to back up HTML and shell script files

# Hacking the Script

First off, if you have a modern version of tar, you might find that it has the ability to read a list of files from stdin (for example, GNU’s tar has a -T flag to have the file list read from standard input). In this case, the script can be shortened by updating how the file list is given to tar.

The file archive can then be unpacked or simply saved, with a mailbox trimmer script run weekly to ensure that the mailbox doesn’t get too big. Listing 10-9 details a sample trimmer script.

```
#!/bin/bash
# trimmailbox--A simple script to ensure that only the four most recent
# messages remain in the user's mailbox. Works with Berkeley Mail
# (aka Mailx or mail)--will need modifications for other mailers!

keep=4 # By default, let's just keep around the four most recent messages.

totalmsgs=$(echo 'x' | mail | sed -n '2p' | awk '{print $2}')

if [ $totalmsgs -lt $keep ] ; then
  exit 0          # Nothing to do
fi

topmsg=$(($totalmsgs - $keep ))

mail > /dev/null << EOF
di-$topmsg
q
EOF

exit 0
```

Listing 10-9: The trimmailbox script, to be used in conjunction with the remotebackup script

This succinct script deletes all messages in the mailbox other than the most recent ones ($keep). Obviously, if you’re using something like Hotmail or Yahoo! Mail for your archive storage, this script won’t work and you’ll have to log in occasionally to trim things.

# #77 Monitoring Network Status

One of the most puzzling administrative utilities in Unix is netstat, which is too bad, because it offers quite a bit of useful information about network throughput and performance. With the -s flag, netstat outputs volumes of information about each of the protocols supported on your computer,