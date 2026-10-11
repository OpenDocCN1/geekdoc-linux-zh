
# File Naming Conventions

Valid filenames may contain *almost* any character. You do have to pay some attention to the names you come up with. Your Linux system allows filenames up to 255 characters in length. How you define filenames can save you a lot of hassle, as I will soon demonstrate.

Some valid filename examples include the following:

- fish
- duck
- program_2.01
- a.out
- `letter.to.mom.who.I.dont.write.often.enough.as.it.is`
- .bash_profile

Notice the last name in particular. It starts with a dot (or a *period*, if you prefer). Normally, this type of file is invisible with a default listing. Starting a filename with a dot is a way to make a file somewhat invisible. This is good to know if you don’t want to burden file listings with a lot of noise. It is also the way that a cracker might hide her tracks should she break into your system—by creating a directory that starts with a dot. To see these so-called dot files, use the `ls` command with the `-a` flag (`ls -a`).

# Listing Files with Emotion!

The `ls` command seems so simple, and yet it has a number of options that can give you tons of information. Change to something like the /etc directory and try these options:

- `cd /etc`
- `ls --color`
- `ls -b`
- `ls -1S`
- `ls -1t`

The first listing shows different types of files and directories in color. The second (`-b`) shows octal representations for files that might have been created with control characters. Depending on the terminal you are using, the default is to show question marks or simply blanks. If you need to access (or delete) the file, it helps to know what it is really called. The third and fourth options control sorting. The `-ls` option gives you a long listing (lots of information) sorted by file size. The last option (`-lt`) sorts by time with the newest files at the top of the list and the oldest at the bottom.

## A Peek at Metacharacters

Metacharacters are special characters that have particular meaning to your shell—the dollar sign or hash mark prompt where you do your work. The two metacharacters I want to look at are the asterisk and the question mark. The following is what they mean to the shell:

- `*` Match any number of characters
- `?` Match a single character

Extending our talk of listing files, you could list all files containing "ackle" by using this command:

```bash
$ ls *ackle*
hackle hackles tackles
```

Similarly, you could find all the words that start with an h like this:

```bash
$ ls h*
hackle hackles
```

Now, if you want to see all the seven-letter words in your directory, use this command:

```bash
$ ls ???????
hackles tackles
```

Each question mark represents a single letter position.

## File Permissions in the Shell

In Chapter 4, I showed you how to look at file permissions with Nautilus. When you use the `ls -l` command, you are doing the same thing: look at basic Linux security at the file (or directory) level. Here is an example of a long `ls` listing:

```bash
$ ls -l
total 3
drwxr-x---  5 root    system   512 Dec 25 12:01 presents
-r-xr--r--  1 zonthar users   123 Dec 24 09:30 wishlist
-rw-rw----  1 zonthar users   637 Nov 15 09:30 griffong
```

The first entry under the total column shows a directory (I'll talk about the next nine characters in a moment). The first character is a d, which indicates a directory. At the end of each line, you find the directory or filename—in my example, they are presents, wishlist, and griffong. Because the first character in the permissions field is d, presents is a directory.

The other nine characters (characters 2 through 10) indicate permissions for the user or owner of the file (first three), the group (second group of three), and others or everyone else (last three). In the first line, user root has read (r), write (w), and execute (x) permissions, whereas the system group has only read and execute. The three dashes at the end imply that no one else has any permissions. The next two files are owned by the user called zonthar.

![](img/0e9cf4c65a042f4a9bea644dc50153a7_409_0.png)

# *Quick Tip*

Remember user, group, and other (`ugo`). You will find them useful later when I cover changing file and directory permissions.

# Not-So-Hidden Files

When you take your first look at valid filenames, remember that I mentioned that files starting with a period are hidden. As a result, creating directories or files in this way is a favorite trick of system crackers. Get used to the idea of listing your directories and files with a `-a` option so that you see everything that’s there. Look for anything unusual.

Keep in mind, however, that a number of applications create dotted directory names in your home directory so that you are generally not burdened with seeing all these configuration areas. That’s great, except that you should know what you’ve got on your disk. Always balance your need for convenience with a healthy curiosity. A quick `ls -a` in your home directory shows you some files (and directories) you will become very familiar with as time goes on. Here is an example of what you will see:

```bash
.Xauthority  .bash_history  .bash_profile  .gnupg  .gnome2
```

# Strange Filenames That Just Don't Go Away

Every once in a while, you do a listing of your directory and some strange file appears that you just know isn't supposed to be there. Don't panic. It's not necessarily a cracker at work. You may have mistyped something and you just need to get rid of the error. The problem is that you can't. Case in point: I accidentally created a couple of files with hard-to-deal-with names. I don't want them there, but trying to delete them does not work. Here are the files:

```bash
-another_file
 onemorefile
```

Here's what happens when I try to delete them:

```bash
$ rm -another_file
rm: invalid option -- a
Try 'rm --help' for more information.
```

What about that other file?

```bash
$ rm onemorefile
rm: cannot remove 'onemorefile': No such file or directory
```

The problem with the first file is that the hyphen makes it look like I am passing an option to the rm command. To get around this problem, I use the double-dash option on the rm command. Using two dashes tells the command that what follows is not an option to that command. Here I go again:

```bash
$ rm -- -another_file
$
```

Bravo! By the way, this double-dash syntax applies to many other commands that need to recognize potentially weird filenames. Now, what about the second file? It looked fine, didn't it? If you look very closely, you see that there is a space in front of the leading o, so simply telling rm to remove the file doesn't work either, because onemorefile is not the filename. It is actually " onemorefile" (preceded by a space). So, I need to pass the space as well; to do that, I give the full name (space included) by enclosing the filename in double quotes.

```bash
$ rm " onemorefile"
$
```

# More on rm (or, "Oops! I didn't really mean that")

When you delete a file with Linux, it is gone. If you didn't really mean to delete (or rm) a file, you quickly find out if you have been keeping good backups. The other option is to check with the rm command before you delete a file. Rather than simply typing rm followed by the filename, try this instead:

```bash
rm -i file_name1 file_name2 file_name3
```

The -i option tells rm to work in interactive mode. For each of the three files in the example, rm pauses and asks if you really mean it.

```bash
rm: remove 'file_name1'?
```

If you like to be more wordy than that, you can also try `rm --interactive file_name`, but that goes against the system administrator's first principle.

![](img/0e9cf4c65a042f4a9bea644dc50153a7_411_0.png)

> **System Administrator's First Principle** Simplifying things. If your solution makes things more complicated, something has gone terribly wrong.

Of course, in following the system administrator's first principle, you could remove all the files starting with the word file by using the asterisk:

```bash
rm -i file*
```

# Making Your Life Easier with alias

You might find that you want to use the -i option every time you delete something, just in case. It's a lot easier to type Y in confirmation than it is to go looking through your backups. The problem is that you are adding keystrokes, and everyone knows that system administrators are notoriously lazy people. Then, there's that whole issue of the first principle—that's why we shortened list to ls, after all. Don't despair, though—Linux has a way. It is the alias command.

```bash
alias rm='rm -i'
```
