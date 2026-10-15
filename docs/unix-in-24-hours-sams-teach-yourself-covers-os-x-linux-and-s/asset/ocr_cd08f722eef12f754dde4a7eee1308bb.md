```
$ grep '^taylor:' /etc/passwd
taylor:*::1001:999:Dave Taylor,,,: /home/taylor:/usr/local/bin/bash
```

That’s what I want! In the /etc/passwd file, fields of information are separated by colons, and the last field is the login shell. As expected, you can see that it’s /usr/local/bin/bash.

One more refinement: Use the cut command to slice out just the login shell rather than seeing all the stuff in the /etc/passwd file:

Click here to view code image

```
$ grep '^taylor:' /etc/passwd | cut -d: -f7
/usr/local/bin/bash
```

In a nutshell, you tell cut to use the : as a field delimiter and then show just the seventh field (which is the login shell—count it for yourself).

5. For fun, I used the preceding cut command as the basis of a command sequence on a busy system to see what shells people were using. The program extracts the last field of each line in the password file and then sorts and counts matches, showing the number of occurrences of the shell, one per line. Ready?

Click here to view code image

```
$ cut -d: -f7 /etc/passwd | sort | uniq -c
1 /abuse
230 /bin/bash
75 /bin/csh
23 /bin/ksh
159 /bin/tcsh
2 /bin/zsh
382 /noshell
3 /usr/local/bin/bash
6 /usr/local/bin/tcsh
```

As you can see, many people have been disabled with the noshell option, and, on this system, bash is the most popular. Also note that apparently two versions of bash and tcsh are present on this system, in two different directories.

# Note

The cut command is a great one to remember when you want to slice a column out of a data file like /etc/passwd. Take a minute and learn more about it with man cut on your system.

When you’ve identified your shell, you can contemplate choosing a different one. I suggest that you try bash if you aren’t using it already because it enables you to try all the examples in the next few lessons for yourself.