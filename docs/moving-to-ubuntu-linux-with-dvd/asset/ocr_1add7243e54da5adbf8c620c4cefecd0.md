# **There’s No Place Like $HOME**

Yeah, I know. It’s a pretty cheesy pun, but I like it.

Because you’ve had a chance to play with a few directory commands, I’d like to take a moment and talk about a very special directory. Every user on your system has a home directory. That directory can be referenced with the $HOME environment variable. To get back to your home directory at any time, simply type **cd $HOME** and no matter where you were, there you are. Actually, you only need to type **cd**, press <Enter>, and you are home. The $HOME is implied.

The $HOME shortcut is great for shell scripts or anytime you want to save yourself some keystrokes. For instance, say you want to copy the file **remote.file** to your home directory and you are sitting in /usr/some_remote/dir. You could use either of the next two commands:

```
cp remote.file /home/my_username
cp remote.file $HOME
```

The second command saves you keystrokes, and the more time you spend doing system administration, the more you will love shortcuts like this. To save the maximum keystrokes, you can also use the tile (-), a special character synonym for $HOME.

```
cp remote.file -
```

# **More on File Permissions**

What you can and can’t do with a file, as defined by your username or group name, is pretty much wrapped up in four little letters. Look at the following listing (using **ls -l**) for an example. The permissions are at the beginning of each line.

```
-rw-r--r--  1 mgagne mgagne     937 May 17 13:22 conf_details
-rwxr-xr-x  1 root   root   45916220 Apr  4 12:25 gimp
-rw-r--r--  1 root   root     826 Feb 12 09:43 mail_test
-rw-r--r--  1 mgagne mgagne   44595 May 17 13:22 sk_open.jpg
```