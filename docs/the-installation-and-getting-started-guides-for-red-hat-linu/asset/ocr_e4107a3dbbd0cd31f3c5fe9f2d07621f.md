+   • Tip: Always make sure you know which working directory you're in before you state the relative path to the directory or file you want to get to. You don't have to worry about your position in the filesystem, though, when you state the absolute path to another directory or file.

Now that you're starting to get the hang of changing directories, see what happens when you change to root's login directory.

```
cd /root
```

Oops... You're not logged in as root, so you're “denied permission” to access that directory.

Denying access to the root and other users' accounts (or login directories) is one way your Linux system prevents accidental or malicious tampering. You'll find out more about file “ownership” and permissions later in this chapter.

Really want to change to the root login? Then you've got to use the su command. Type this series of commands:

```
[billy@localhost billy] su root
Password: (your root password)
[root@localhost billy]# cd /root
[root@localhost /root]#
```

As soon as you give the root password, you'll see the changes in your command prompt to show your new, superuser status: the root account designation at the front of the prompt and # at the end (as shown in Figure 16-4).