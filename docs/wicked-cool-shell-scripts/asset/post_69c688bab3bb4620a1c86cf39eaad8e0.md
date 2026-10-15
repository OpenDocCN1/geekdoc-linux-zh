
## Listing 9-8: The apm-footer.html file used to add a section for creating new users

You'll likely want to save this script in the same directory you want to protect with passwords, although you can also put it in your cgi-bin directory as we have done. Either way, make sure you tweak the htpasswd and directory values at the beginning of the script as appropriate. You'll also need an .htaccess file that defines access permissions and an .htpasswd file that exists and is writable by the user who runs the Apache web server on your system.

When you use apm, make sure the first account you create is admin so you can use the script upon subsequent invocations! There's a special test in the code that allows you to create the admin account if .htpasswd is empty.

The result of running the apm script is shown in Figure 9-1. Notice that it not only lists each account but also offers options for adding another account, changing the password of an existing account, deleting an account, or listing all the accounts.

![](img/4ffb1cc24a1b24b49254839643abedb2_259_0.png)

### Hacking the Script

The Apache htpasswd program offers a nice command line interface for appending the new account and encrypted password information to the account database. But only one of the two commonly distributed versions of htpasswd supports batch use for scripts—that is, feeding the script both an account and password from the command line. It’s easy to tell whether your version does: if htpasswd doesn’t complain when you try to use the -b flag, you’ve got the better, more recent version. Chances are you will be good, though.

Be warned that if this script is incorrectly installed, anyone who gains knowledge of the URL can then add themselves to the access file and delete everyone else. That’s not good. One solution is to only allow this script to be run if the user is already signed in as admin (as the commented code in the top of the script mentions). Another way to secure the script is to place it in a directory that itself is password protected.

## #72 Syncing Files with SFTP

Though the ftp program is still available on most systems, it’s being replaced more and more by new file transfer protocols such as rsync and ssh (secure shell). There are a few reasons for this. Since the first edition of this book, FTP has begun to show some weaknesses with scaling and securing data in this new world of “big data,” and more efficient protocols for transferring data have become more mainstream. By default, FTP also transmits data in plaintext, which is generally fine for home or corporate networking on trusted networks, but not if you’re doing an FTP transfer from an open network at, for example, the library or Starbucks, where a lot of people are sharing the same network as you.

All modern servers should support the considerably more secure ssh package supporting end-to-end encryption. The file transfer element of the encrypted transfer is sftp, and while it’s even more primitive than ftp, we can still work with it. Listing 9-9 shows how we can utilize sftp to securely sync our files.

### NOTE

> If you don’t have ssh on your system, complain to your vendor and administrative team. There’s no excuse. If you have access rights, you can also obtain the package at http://www.openssh.com/ and install it yourself.

### The Code

```
#!/bin/bash
# sftpsync--Given a target directory on an sftp server, makes sure that
# all new or modified files are uploaded to the remote system. Uses
# a timestamp file ingeniously called .timestamp to keep track.
timestamp=".timestamp"
tempfile="/tmp/sftpsync.$$"
count=0

trap "$(which rm) -f $tempfile" 0 1 15    # Zap tempfile on exit

if [ $# -eq 0 ] ; then
    echo "Usage: $0 user@host [ remotedir ]" >&2
    exit 1
fi

user="$(echo $1 | cut -d@ -f1)"
server="$(echo $1 | cut -d@ -f2)"

if [ $# -gt 1 ] ; then
    echo "cd $2" >> $tempfile
fi

if [ ! -f $timestamp ] ; then
    # If no timestamp file, upload all files.
    for filename in *
    do
        if [ -f "$filename" ] ; then
            echo "put -P \"${filename}\"" >> $tempfile
            count=$(( $count + 1 ))
        fi
    done
else
    for filename in $(find . -newer $timestamp -type f -print)
    do
        echo "put -P \"${filename}\"" >> $tempfile
        count=$(( $count + 1 ))
    done
fi

if [ $count -eq 0 ] ; then
    echo "So: No files require uploading to $server" >&2
    exit 1
fi

echo "quit" >> $tempfile

echo "Synchronizing: Found $count files in local folder to upload."

if ! sftp -b $tempfile "$user@$server" ; then
    echo "Done. All files synchronized up with $server"
    touch $timestamp
fi
exit 0
```

Listing 9-9: The sftpsync script
