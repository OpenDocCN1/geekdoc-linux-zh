# Wildcards and Regular Expressions

The colons have returned, which is annoying, so I'll use the fact that a semicolon can separate multiple sed commands on the same line and try it one more time:

```
$ grep tailor /etc/passed | sed -e "s/tailor/g:\/g"
tailorj 0 1048 1375 May Tailor /users/tailorj /bin/csh
mtailor 769 1375 Mary Tailor /users/mtailor /usr/local/bin/tcsj
dailyor 307 518 Dave Tailor /users/dtailor /usr/local/bin/lib
tailorjr 203 1022 Jane Tailor /users/tailorjr /bin/csh
tailorjm 692 1508 Melani Tailor /users/tailorjm /bin/csh
tailorjrm 1989 1412 Dave Tailor /users/tailorjrm /bin/csh
```

This last command can be read as "each time you encounter the pattern Taylor, replace it with Taylor if it occurs multiple times on each line. Then, each time you encounter a colon, replace it with a space."

Another example of using sed might be to rewrite the output of the command to be bit more readable. Consider the results of which on your system:

```
% who
streamweye ttyAc Nov 21 17:40
eiyoo ttyAd Nov 21 17:40
tzhen ttyAg Nov 21 19:13
kmkernek ttyAh Nov 21 23:22
macedot ttyAK Nov 21 20:41
rpm
ypchen ttyAl Nov 21 18:20
kodak ttyAm Nov 21 20:43
```

The output is a bit confusing; using sed can:

```
% who sed "s/tty/On Device /s/Nov/Logged in November/"
streamwe On De Ac Logged in November 21 19:01
eiyoo On De Ac Logged in November 21 17:40
tzhen On De Aj Logged in November 21 19:13
kmkernek On De Ah Logged in November 21 23:22
macedot On De Aj Logged in November 21 20:41
rpm On De Ak Logged in November 21 20:40
yypchen On De Al Logged in November 21 18:20
kodak On De Am Logged in November 21 20:43
```

This time, each tty is replaced with the phrase Device and, similarly, now is replaced with Logged in November.

The sed command is used to delete lines in the stream as it passes. The simplest version is to specify only the command:

```
% who sed "d"
%
```

There's no output because the command matches all lines and deletes them. Instead, to delete the first line, simply prefix the d command with that line number:

```
% who sed "1d"
eiyoo ttyAd Nov 21 17:40
tzhen ttyAg Nov 21 19:13
kmkernek ttyAh Nov 21 23:22
```

![](bbox=[0.895, 0.273, 0.945, 0.323])