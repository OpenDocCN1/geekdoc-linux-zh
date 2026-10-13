The whereis command shows that the time binary is located in /usr/bin/time, whereas the header file is in /usr/include/time.h. Two man page paths are also returned. If you're interested in finding where programs and their associated files are located on your machine, whereis might do the trick.

# which

Lastly, the which command can also help you locate files that are contained within one of the directories specified in your PATH environment variable. Lesson 16, "Modifying the User Environment," discusses how you can go about configuring the PATH variable. This is less useful as a method of finding files than as a way to find out which version of a program executes when you type a command. For example, if your system has two different programs named time, you can use the which command to find out which one runs when you type time. You can invoke which much like you did whereis—just supply a filename for it to look up.

For example:

```
>which time
/usr/bin/time
```

UNIX returns the full path to the time command. The which command is the least configurable of the commands you've seen so far, but it is also the fastest. If you're ever trying to remember where a program is located, give which a shot.

# FINDING FILES THAT CONTAIN A WORD OR PATTERN

One of the most powerful built-in programs in UNIX is grep. The grep utility enables you to quickly search through the body of files for a particular word or pattern. grep comes in three flavors: grep, egrep, and fgrep. The differences between these versions are based on the complexity of the regular expressions that they can handle. Regular expressions define a pattern of text that can be used to search files when a specific word or phrase to be searched for might not be known. (You will learn more about regular expressions in Lesson 13, "Regular