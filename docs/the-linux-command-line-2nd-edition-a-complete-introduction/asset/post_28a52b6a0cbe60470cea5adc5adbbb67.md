
```
${parameter/pattern/string}
${parameter//pattern/string}
${parameter/#pattern/string}
${parameter/%pattern/string}
```

This expansion performs a search-and-replace upon the contents of parameter. If text is found matching wildcard pattern, it is replaced with the contents of string. In the normal form, only the first occurrence of pattern is replaced. In the // form, all occurrences are replaced. The /# form requires that the match occur at the beginning of the string, and the /% form requires the match to occur at the end of the string. /string may be omitted, which causes the text matched by pattern to be deleted.

```
[me@linuxbox ~]$ foo.JPG.JPG
[me@linuxbox ~]$ echo ${foo/JPG/jpg}
jpg.JPG
[me@linuxbox ~]$ echo ${foo//JPG/jpg}
jpg.jpg
[me@linuxbox ~]$ echo ${foo/#JPG/jpg}
JPG.JPG
[me@linuxbox ~]$ echo ${foo/%JPG/jpg}
JPG.jpg
```

Parameter expansion is a good thing to know. The string manipulation expansions can be used as substitutes for other common commands such as sed and cut. Expansions improve the efficiency of scripts by eliminating the use of external programs. As an example, we will modify the longest-word program discussed in the previous chapter to use the parameter expansion ${#j} in place of the command substitution $(echo $j | wc -c) and its resulting subshell, like so:

```
#!/bin/bash

# longest-word3 : find longest string in a file

for i; do
    if [[ -r $i ]]; then
        max_word=
        max_len=
        for j in $(strings $i); do
            len=${#j}
            if (( len > max_len )); then
                max_len=$len
                max_word=$j
            fi
        done
        echo "$1: '$max_word' ($max_len characters)"
    fi
    shift
done
```

Next, we will compare the efficiency of the two versions by using the time command:

```
[me@linuxbox ~]$ time longest-word2 dirlist-usr-bin.txt
dirlist-usr-bin.txt: 'scrollkeeper-get-extended-content-list' (38 characters)

real 0m3.618s
user 0m1.544s
sys 0m1.768s
[me@linuxbox ~]$ time longest-word3 dirlist-usr-bin.txt
dirlist-usr-bin.txt: 'scrollkeeper-get-extended-content-list' (38 characters)

real 0m0.060s
user 0m0.056s
sys 0m0.008s
```

The original version of the script takes 3.618 seconds to scan the text file, while the new version, using parameter expansion, takes only 0.06 seconds—a very significant improvement.

## Case Conversion

Recent versions of bash have support for upper/lowercase conversion of strings. bash has four parameter expansions and two options to the declare command to support it.

So what is case conversion good for? Aside from the obvious aesthetic value, it has an important role in programming. Let's consider the case of a database look-up. Imagine that a user has entered a string into a data input field that we want to look up in a database. It's possible the user will enter the value in all uppercase letters or lowercase letters or a combination of both. We certainly don't want to populate our database with every possible permutation of upper and lower case spellings. What to do?

A common approach to this problem is to normalize the user's input. That is, convert it into a standardized form before we attempt the database look-up. We can do this by converting all of the characters in the user's input to either lower or uppercase and ensure that the database entries are normalized the same way.

The declare command can be used to normalize strings to either upper or lowercase. Using declare, we can force a variable to always contain the desired format no matter what is assigned to it:

```
#!/bin/bash

# ul-declare: demonstrate case conversion via declare

declare -u upper
declare -l lower

if [[ $1 ]]; then
    upper="$1"
    lower="$1"
    echo $upper
    echo $lower
fi
```

In the above script, we use declare to create two variables, upper and lower. We assign the value of the first command line argument (positional parameter 1) to each of the variables and then display them on the screen:

```
[me@linuxbox ~]$ ul-declare aBc
ABC
abc
```

As we can see, the command line argument ("aBc") has been normalized.

There are four parameter expansions that perform upper/lowercase conversion:

### Table 34-1: Case Conversion Parameter Expansions

| Format | Result |
|---|---|
| ${parameter,,} | Expand the value of parameter into all lowercase. |
| ${parameter,} | Expand the value of parameter changing only the first character to lowercase. |
| ${parameter^^} | Expand the value of parameter into all uppercase letters. |
| ${parameter^} | Expand the value of parameter changing only the first |
