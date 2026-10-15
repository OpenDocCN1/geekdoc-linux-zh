
# EXAMPLE 12.15

(The Script)

```
read answer
```

```
1 if [[ $answer = [Yy]* ]]    # Test for Yes or yes or Y or y, etc.
then...
```

Example:
(The Script)

```
guess=Noone
```

```
2 if [[ $guess != [Nn]o{one|body} ]]    # Test for Noone, noone, or Nobody, nobody...
then...
```

Example:
(The Command Line)

```
3 [[ apples < oranges ]]
print $? 
0
```

```
4 [[ apples > oranges ]]
print $? 
1
```

```
5 $ name="Joe Shmoe"
$ [ $name = "Abe Lincoln" ]
ksh: Shmoe: unknown test operator
# old style
```

```
6 $ [[ $name = "Abe Lincoln" ]]
$ echo $?
1
# new style
```

# EXPLANATION

+   1 The answer read in from the user is tested to see if it matches anything starting with Y or y.
+   2 The variable guess is tested. If it is not equal to a string starting with N or n, followed by an o, and exactly one or body (for example, noone or nobody) the then command would be executed.
+   3 The string apples is tested to see if it comes before oranges in the ASCII collating sequence. It does.
+   4 The string apples is tested to see if it comes after oranges in the ASCII collating sequences. It does not.
+   5 In the old-style test, the variable name is split into separate words. Because the = operator expects a single string as its left operand, the test command fails. To fix the problem, the variable should be enclosed in double quotes.
+   6 In the new-style test, the variable is not split up into separate words; therefore, double quotes are not required around $name.

# 12.5.4 File Testing with Binary Operators

The binary operators for testing files require two operands (i.e., a file on either side of the operator). See Table 12.8 for a list of binary file-testing operators.

# Table 12.8 Binary File Testing and Logical Operators

| Operator | Tests For |
|---|---|
| file1 -nt file2 | True if file1 is newer than file2 |
| file1 -ot file2 | True if file1 is older than file2 |
| file1 -ef file2 | True if file1 is another name for file2 |

# 12.5.5 Expression Testing with Logical Operators

The Korn shell, like C, provides logical testing of the truth or falsity of expressions. They are listed in Table 12.9.

# Table 12.9 Logical Operators

| Operator | Tests For |
|---|---|
| && | The AND operator evaluates the expression on the left-hand side of &&, if true, the expression on the right side of && is tested and must also be true. If one expression is false, the expression is false. The && operator replaces -a; for example, (( $x && $y ) > 5 ). |
| || | The OR operator evaluates the expression on the left-hand side of the || operator; if true, the expression is true; if false, the expression on the right-hand side of the || is evaluated; if true, the expression is true. Only if both expressions are false will the expression evaluate to false. The || operator replaces -o; for example, (( $x || $y ). |

# 12.5.6 File Testing with Flags

The Korn shell provides a number of built-in test commands for checking the attributes of files, such as existence, type, permissions, and so forth. The file-testing options (also called flags) are listed in Table 12.10.

# Table 12.10 File Testing (New test Flags)

| Flag | Tests For |
|---|---|
| Korn Shell Only | |
| -a file | file exists |
| -e file | file exists (versions newer than 1988) |

# Table 12.10 File Testing (New test Flags) (continued)

| Flag | Tests For |
|---|---|
| -L file | file exists and is a symbolic link |
| -O file | You are the owner of file |
| -G file | Your group ID is the same as files |
| -S file | file exists and is a socket |

# Bourne and Korn Shells

| Flag | Tests For |
|---|---|
| -b file | file exists and is a block special file |
| -c file | file exists and is a character special file |
| -d file | file exists and is a directory |
| -f file | file exists and is not a directory |
| -g file | file exists and is setgid |
| -k file | file exists and sticky bit is set |
| -p file | file exists and is a named pipe |
| -r file | file exists and is readable |
| -s file | file has a nonzero size |
| -u file | file exists and is setuid |
| -w file | file exists and is writable |
| -x file | file exists and is executable |

# EXAMPLE 12.16

```
(The Script)
1 file=/etc/passwd
2 if [[ -f $file && (-r $file || -w $file) ]]
   then
3   print $file is a plain file and is either readable or writable
fi
```

# EXPLANATION

+   1. The variable file is assigned /etc/passwd
+   2. The file test operators test if the file is a plain file and is either readable or writable. The parentheses are used for grouping. In the old test, the parentheses had to be escaped with a backslash.
+   3. If both of the tests are true, the file is a plain file, and it is either readable or writable, this line is executed.
