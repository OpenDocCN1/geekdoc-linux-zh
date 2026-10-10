```
#
testuser=christine
#
if [ $testuser = christine ]
then     echo "The testuser variable contains: christine"
else     echo "The testuser variable contains: $testuser"
fi
$
$ ./string_test.sh
The testuser variable contains: christine
$
```

Also, using the not equals string comparison allows you to determine whether or not two strings have the same value:

```
$ cat string_not_test.sh
#!/bin/bash
# Using string test not equal evaluations
#
testuser=rich
#
if [ $testuser != christine ]
then     echo "The testuser variable does NOT contain: christine"
else     echo "The testuser variable contains: christine"
fi
$
$ ./string_not_test.sh
The testuser variable does NOT contain: christine
$
```

Keep in mind that the test comparison takes all punctuation and capitalization into account when comparing strings for equality.

# **Looking at string order**

Trying to determine if one string is less than or greater than another is where things start getting tricky. Two problems often plague shell programmers when they're trying to use the greater-than or less-than features of test conditions:

+   ▪ The greater-than and less-than symbols must be escaped, or the shell uses them as redirection symbols, with the string values as