
Or I could use this regular expression:

```
$ ls [ab]*
aa.txt  ac.txt  a.txt  b.txt
```

When I put a set of characters inside brackets, this sets up a character class. A character class defines a set of characters that will match. It’s important to note that this character class matches only one character. So why use this when a shell glob can accomplish the same thing? I find I use it often when I’m trying to manage a directory full of logs. When logs in /var/log/ rotate, they end up appending a number to the file and then compressing it. For instance:

```
$ ls /var/log/messages*
/var/log/messages      /var/log/messages.2.gz
/var/log/messages.5.gz  /var/log/messages.3.gz
/var/log/messages.6.gz
/var/log/messages.1.gz  /var/log/messages.4.gz
```

Often you will find when you need to free up space on a disk that /var/log is a good place to start. Let’s say that I wanted to remove only the last three messages logs. While I could certainly type them all in manually, I could also type

```
$ rm /var/log/messages.[456].gz
```

> NOTE As you learn about shell globs and regular expressions, you will find out that often the pattern you match is different from the pattern you thought you’d match. To be safe, always run ls or echo with your pattern first and see what files match before you do something like mv or rm, which are difficult or almost impossible to undo.

## Pipes and Redirection

### Pipes

If there is one tool that I think best illustrates the power of the command line, it’s the pipe. If you look at a lot of command examples, one of the first things you will see is the | symbol. This is known as a pipe and is used to take the output from one program and feed it to another program as input. You can use pipes to chain multiple commands together so that one command generates output, and the next command filters through that output and changes it and then outputs it to some other program.

**grep** One of the best examples of the use of pipes is also one of the most useful command-line tools: grep. At its core, the grep command filters its input for a keyword or pattern that you specify and then outputs anything that matches that pattern. For instance:

```
$ ls
anotherfile.txt somedir somefile1.txt somefile2.txt
$ ls | grep some
somedir
somefile1.txt
somefile2.txt
```

In the second command you can see that I piped the output of the ls command to grep, and then told grep to filter only text that contained the keyword some. If I had wanted to see only text that had the word file in it, I could type

```
$ ls | grep file
anotherfile.txt
somefile1.txt
somefile2.txt
```

You can also chain multiple grep commands together using pipes. For instance, say after I ran the command above I decided that I wanted to filter the output again, only this time to show only files that contained 1 in their name:

```
$ ls | grep file | grep 1
somefile1.txt
```

You will often see grep used in this way to filter output from one command and pipe it to another command to act on the new filtered input. grep can also be used to filter text that is inside a file. Just continue to list your keyword as the first argument to grep and then follow it with the file to filter through. For instance, let’s say our somefile1.txt file contained the following lines:

- 1. Line 1
- 2. Another line
- 3. Final line
- 4. Some other text

If I wanted to see any lines that contained the word line, I would type

```
$ grep line somefile1.txt
2. Another line
3. Final line
```

Now notice that it didn’t display 1. Line 1. That’s because in that case the l in Line was capitalized and by default grep is case-sensitive. If you want to do a case-insensitive match, then use grep with the -i argument:

```
$ grep -i line somefile1.txt
1. Line 1
2. Another line
3. Final line
```

You will find you use grep a lot to search through log files for particular keywords. Sometimes, though, as you filter through certain keywords you will notice you get extra output that you aren’t interested in. If you pass the -v argument to grep, it will invert what it does; that is to say, it will show you only lines that don’t match your keyword. For instance, in the same somefile1.txt that I listed above, let’s say that I wanted to show all of the lines that didn’t contain the word Another:

```
$ grep -v Another somefile1.txt
1. Line 1
3. Final line
4. Some other text
```

**sort** Another useful command-line tool is sort. As its name indicates, the sort command takes input and sorts it. For instance, let’s take two files, somefile2.txt:
