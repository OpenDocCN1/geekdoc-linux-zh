take the output from one program and feed it to another program as input. You can use pipes to chain multiple commands together so that one command generates output, and the next command filters through that output and changes it and then outputs it to some other program.

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

You will often see grep used in this way to filter output from one command and pipe it to another command to act on the new filtered input. grep can also be used to filter text that is inside a file. Just continue to list your keyword as the first argument to grep and then follow it with the file to filter