```
test4.sh is a file
test5.sh is a file
test6.sh is a file
test7.sh is a file
today.txt is a file
Videos is a directory
$
```

That saves a lot of coding from having to check each file manually in a bunch of if or case statements.

When working with files in a directory, it's common to use wildcard characters to specify a range of files. There are three methods you can choose from:

+   - A question mark (?) represents one character.Thus, c?t would match cat, cot, and cut.
+      - An asterisk (*) represents any character, multiple characters, or even no characters.Thus, c*t would match cat, caveat, and ct.
+      - A bracketed set of characters matches only the characters in the brackets. Thus, c[au]t would match cat and cut, but not cot.

This method of using wildcard characters for filenames is also called file glob-bing and can be used in any situation where you iterate through multiple files.

# The while Loop

Another useful loop statement is the while command. This is its format:

```
while [ condition ] ; do
commands
done
```

The while loop keeps looping as long as the condition specified evaluates to a True logical value. When the condition evaluates to a False logical value, the looping stops. The condition used in the while loop is the same as that for the if statement, so you can test numbers, strings, and files. Listing 25.14 demonstrates using the while loop to calculate the factorial of a number.

**Listing 25.14:** Calculating the factorial of a number

```
$ cat test8.sh
#!/bin/bash
number=$1
```