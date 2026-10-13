The next step is to transliterate all capitalized versions of words to the lowercase version because words such as To and to and The and the are really the same word. You can do this by using tr to change all the capital characters 'A'-'Z' into lowercase characters 'a'-'z' as follows:

```
$ tr '[:[:upper:]]' '[:lower:]' < ch15.doc | tr 'A'-'Z' 'a'-'z'
```

Here you pipe the output of the first tr command into a second tr command. The input to the first tr command is the file ch15.doc, whereas the input to the second tr command is the output of the first tr command.

# Differences Between tr Versions

In this example, you are using a single space for set2. Most versions of tr interpret this to mean transliterating all the characters in set1 to a space. Some versions of tr do not do this.

You can determine whether your version of tr works correctly using the following test:

```
$ echo 'Hello, my dear' | tr ',! ' ' '
```

Most versions of tr produce the following output:
Hello my dear

Some versions produce the following output instead:
Hello my dear!

To obtain the desired behavior from these versions of tr, make sure that set1 and set2 have the same number of characters. In this case, set2 needs to contain two spaces:

```
$ echo 'Hello, my dear' | tr ',! ' '  '
```

# Squeezing Out Spaces

At this point, several of the lines have multiple spaces separating the words. You need to reduce or squeeze these multiple spaces into single spaces to avoid problems generating counts later. To do this, you need to use the -s (short for squeeze) option of the tr command. The basic syntax is

```
tr -s set1
```

When tr encounters multiple consecutive occurrences of a character in set1, it replaces these with only one occurrence of the character. For example,