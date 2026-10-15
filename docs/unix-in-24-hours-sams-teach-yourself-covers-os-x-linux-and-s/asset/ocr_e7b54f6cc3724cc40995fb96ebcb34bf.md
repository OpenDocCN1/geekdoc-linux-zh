directories within those. This is true with Dropbox, OneDrive, iCloud, and any other Unix-compatible cloud storage system you might have configured, even those internal to your corporation. I'll show you what I mean later in the lesson!

The command for creating directories is actually one of the least complex and most mnemonic (for Unix, anyway) in this book: mkdir, for “make directory.”

Note

Pronounce the mkdir command as “make-drrr.”

+   1. Move to your home directory and examine the files and directories there. Here’s an example:

Click here to view code image

```
% cd
% ls -F
Archives/          OWL/               rumors.26Oct.Z
InfoWorld/         PubAccessLists.Z   rumors.5Nov.Z
LISTS              bin/               src/
Mail/              educ
News/              mailing.lists.bitnet.Z
```

+   2. To create a directory, specify what you’d like to name the directory and where you’d like to locate it in the file system (the default location is your current working directory):

Click here to view code image

```
% mkdir NEWDIR
% ls -F
Archives/          News/              mailing.lists.bitnet.Z
InfoWorld/         OWL/               rumors.26Oct.Z
LISTS              PubAccessLists.Z   rumors.5Nov.Z
Mail/              bin/               src/
NEWDIR/            educ
```

Note

Although Unix is very flexible about file and directory names, as a general rule, you’ll want to avoid spaces, tabs, control characters, and the / character because they’ll make things more difficult later on.

+   3. That’s all there is to it. You’ve created your first Unix directory, and you can now list it with ls to see what it looks like:

Click here to view code image

```
% ls -ld NEWDIR
drwxrwx- 2 taylor     24 Nov  5 10:48 NEWDIR
% ls -la NEWDIR
total 2
drwxrwx- 2 taylor     24 Nov  5 10:48 .
drwx-- 11 taylor    1024 Nov  5 10:48 ..
```

Remember that the -d flag to ls specifies that it should show the directory itself, not the contents of the directory. Try it both ways, and you’ll immediately see the