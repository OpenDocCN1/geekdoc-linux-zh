# Chapter 12: Using Structured Commands

fi
$
$ ./string_test.sh
The tester variable contains: christine
$
Also, using the not equals string comparison allows you to determine whether or not two strings have the same value:

```
$ cat string_not_test.sh
#!/bin/bash
# Using string test not equal evaluations
# 
tester=rich
#
if [ $tester != christine ]
then
    echo "The tester variable does NOT contain: christine"
else
    echo "The tester variable contains: christine"
fi
$
$ ./string_not_test.sh
The tester variable does NOT contain: christine
$
Keep in mind that the test comparison takes all punctuation and capitalization into account when comparing strings for equality.

**Looking at string order**

Trying to determine if one string is less than or greater than another is where things start getting tricky. Two problems often plague shell programmers when they're trying to use the greater-than or less-than features of test conditions:
```

+   The greater-than and less-than symbols must be escaped, or the shell uses them as redirection symbols, with the string values as filenames.
+   The greater-than and less-than order is not the same as that used with the `sort` command.

The first item can result in a huge problem that often goes undetected when programming your scripts. Here's an example of what sometimes happens to novice shell script programmers:

```
$ cat bad_string_comparison.sh
#!/bin/bash
# Misuing string comparisons
# 
string1=soccer
string2=zorbfotball
#
if [ $string1 > $string2 ]
then
    echo "$string1 is greater than $string2"
```