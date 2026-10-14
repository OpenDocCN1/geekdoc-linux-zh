and will get some sort of error message like “too many arguments.” There are a limited number of arguments you can have in your shell, but luckily if this happens to you, there is a good way around it using the xargs program. The xargs program will accept a set of arguments that are piped to it and will run a command against those arguments one by one. So, for instance, if I got that error in my find command, I could instead type

```
$ find ./ -name "*.txt" -print0 | xargs mv ~/Documents
```

# Use Your Bash History

While it’s always advisable to document all of your procedures, especially when you fix a problem, sometimes you don’t get around to it and have to figure out what you did the last time to fix a system. It can be easy to forget that bash logs all of your previous commands to its history file. One of the first things I do when I can’t remember exactly how I ran a command previously is type history and look through the output for more details.

# Are These Files Identical?

As you troubleshoot problems on a system, you commonly wonder whether the problem stems from one server having a different configuration file from another working server. While you can definitely open both files and compare them line by line or run diff against them, both methods can be tedious. A quick way to test whether two files are identical is to use the md5sum tool to create a checksum of both. If the output matches, the files are identical:

```
$ md5sum bar
 d41d8cd98f00b204e9800998ecf8427e  bar
$ md5sum foo
 d41d8cd98f00b204e9800998ecf8427e  foo
```

# Go Back to Your Previous Directory

This is a nice quick tip. When you move around directories on a system, sometimes it would be nice if you could quickly jump back to the directory you were previously in. Just type

```
$ cd -
```