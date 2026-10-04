```
text:
    338 motd    340 passwd
```

One side effect of the mv command, which is actually used more than its ability to move files around between directories, is the fact that if the new file is in the same directory as the old file then it performs the same function as a rename command. In fact there is no specific rename command in Linux; you just use mv:

```
$ mv backup/motd2.bak backup/motd.sym.link
$ ls -i backup
    338 motd.bak    328 motd.sym.link 340 passwd.bak
```

Just as with the cp command, mv can have its second parameter specified as a directory rather than a file and the first parameter can then be a list of files, all of which will be moved into the specified directory, whilst keeping the same file names as before.

# 2.3 Manipulating Files

Very often, you will want to examine the contents of a text file. You have already seen one method for doing this – using the cat command. The word cat is an abbreviation of the word concatenate, which means to join together. The way in which the cat command achieves this joining is by allowing you to specify a list of file names as parameters which it will list one after the other without a break:

```
$ cat /etc/passwd /etc/motd
```

The problem with this is that if the contents of the files you list to the screen are longer than one screenful, then the whole thing just scrolls past too fast to read and you end up only seeing the last screen full at the end of the listing. What you require is a command which lists files like cat but which will insert pauses at the end of each screen full. The usual command to do this is called more:

```
$ more /etc/passwd /etc/motd
```

When more pauses at the end of a page there are several characters you can type to tell it what to do next:
Space list next page;
Enter list next line;
q quit listing;
:n list next file.

Another command that works like more but which provides a whole host of facilities in addition to those available with more is (amusingly) called less.