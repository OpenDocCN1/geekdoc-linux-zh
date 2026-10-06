# Part III Advanced Shell Scripting

Next comes the three digit area code. In the United States area codes start with the number 2 (no area code use the digits 0 or 1), and can go to 9. To match the area code, you'd use the pattern:

```
[2-9][0-9][2]
```

This requires that the first character be a digit between 2 and 9, followed by any two digits. After the area code, the ending right parenthesis may or may not be:

```
\?
```

After the area code there can be a space, no space, a dash, or a dot. You can group those using a character group along with the pipe symbol:

```
( |\.)
```

The first pipe symbol appears immediately after the left parenthesis to match the no space condition. you must use the escape character for the dot; otherwise, it'll take on its special meaning of matching any character.

Next comes the three-digit phone exchange number. Nothing special required here:

```
[0-9](3)
```

After the phone exchange number, you must match either a space, a dash, or a dot (this time you don't have to worry about matching no space, since there must be at least a space between the phone exchange number and the rest of the number):

```
( |\.)
```

To finish things off, you must match the four digit-local phone extension at the end of the string:

```
[0-9](4)
```

Putting the every pattern results in this:

```
^\([2-9][0-9](2)\)?(| |\.)[0-9](3)(|\.)[0-9](4)$
```

You can use this regular expression pattern in the awk program to filter out bad phone numbers. All you need to do now is create a simple script using the regular expression in a gawk program, then filter your phone list through the script. Remember, when you use regular expression intervals in the gawk program you must use the --re-interval command line option or you won't get the correct results.

Here's the script:

```
$ cat isphone
#!/bin/bash
# script to filter out bad phone numbers
gawk --re-interval '/^\([2-9][0-9](2)\)?(| |\.)[0-9](3)(|\.)[0-9](4)/(print $0)'
$
```

468