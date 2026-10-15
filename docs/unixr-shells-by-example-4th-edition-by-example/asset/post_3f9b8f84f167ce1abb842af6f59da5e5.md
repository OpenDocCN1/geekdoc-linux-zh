
## EXPLANATION

+   1. The output of the rusers command is piped to awk. If the regular expression tom is found, awk prints the first field. The first field, in this case, is the name of the machine(s) where user tom is logged on.
+   2. User tom is logged on three machines. The names of the machines are displayed.
+   3. The number of elements in the array is accessed by preceding the array name with $#. There are three elements in the array.
+   4. The last element of the array is displayed. The number of elements in the array ($#machine) is used as a subscript.
+   5. The array is displayed.
+   6. The shift command shifts the array to the left. The first element of the array is dropped and the subscripts are renumbered, starting at 1.
+   7. The first element of the array after the shift is displayed.
+   8. After the shift, the length of the array has decreased by one.

## 9.12 Quoting

The C/TC shell has a whole set of metacharacters that have some special meaning. In fact, almost any character on your keyboard that is not a letter or a number has some special meaning for the shell. Here is a partial list:

* ? [ ] $ - | ^ & { } ( ) > < | ; : %

The backslash and quotes are used to escape the interpretation of metacharacters by the shell. Whereas the backslash is used to escape a single character, the quotes can be used to protect a string of characters. There are some general rules for using quotes:

+   1. Quotes are paired and must be matched on a line. The backslash character can be used to escape a newline so that a quote can be matched on the next line.
+   2. Single quotes will protect double quotes, and double quotes will protect single quotes.
+   3. Single quotes protect all metacharacters from interpretation, with the exception of the history character (!).
+   4. Double quotes protect all metacharacters from interpretation, with the exception of the history character (!), the variable substitution character ($), and the backquotes (used for command substitution).

### 9.12.1 The Backslash

The backslash is used to escape the interpretation of a single character and, in the C shell, is the only character that can be used to escape the history character, the exclamation point (also called the bang). Often the backslash is used to escape the newline character. Backslash interpretation does not take place within quotes.

## EXAMPLE 9.63

```
1 % echo Who are you?
echo: No match.
2 % echo Who are you\?
who are you?
3 % echo This is a very,very long line and this is where \
break the line.
This is a very, very long line and this is where
I break the line.
4 % echo "\\abc
\\|abc
% echo '\abc'
\\|abc
% echo \\abc
\\abc
5 % echo Wow\!
Wow!
```

## EXPLANATION

+   1 The question mark is used for filename expansion. It matches for a single character. The shell is looking for a file in the current directory that is spelled y-o-u, followed by a single character. Because there is not a file by that name in the directory, the shell complains that it could not find a match with No match.
+   2 The shell will not try to interpret the question mark, because it is escaped with the backslash.
+   3 The string is continued to the next line by escaping the newline with a backslash.
+   4 If the backslash is enclosed in either single or double quotes, it is printed. When not enclosed in quotes, the backslash escapes itself.
+   5 The exclamation point must be escaped with a backslash. Otherwise the C shell will perform history substitution.

### 9.12.2 Single Quotes

Single quotes must be matched on the same line and will escape all metacharacters with the exception of the history (bang) character (!). The history character is not protected because the C shell evaluates history before it does quotes, but not before backslashes.

## EXAMPLE 9.64

```
1 % echo 'I need $5.00'
I need $5.00
2 % echo 'I need $500.00 now\!\!'
I need $500.00 now!!
```

## EXAMPLE 9.64 (CONTINUED)

```
3 % echo 'This is going to be a long line so
Unmatched '.
4 % echo 'This is going to be a long line so \
I used the backslash to suppress the newline'
This is going to be a long line so
I used the backslash to suppress the newline
```

## EXPLANATION

+   1 The string is enclosed in single quotes. All characters, except the history (bang) character (!), are protected from shell interpretation.
+   2 The !! must be protected from shell interpretation by using the backslash character.
+   3 The quotes must be matched on the same line, or the shell reports Unmatched '.
+   4 If the line is to be continued, the backslash character is used to escape the newline character. The quote is matched at the end of the next line. Even though the shell ignored the newline, the echo command did not.

### 9.12.3 Double Quotes

Double quotes must be matched, will allow variable and command substitution, and hide everything else except the history (bang) character (!). The backslash will not escape the dollar sign when enclosed in double quotes.

## EXAMPLE 9.65

```
1 % set name = Bob
% echo "Hi $name"
Hi Bob
2 % echo "I don't have time."
I don't have time.
3 % echo "WOH!"  # Watch the history metacharacter!
%: Event not found.
4 % echo "whoopie!"!
Whoopie!
5 % echo "I need \$5.00"
I need \$5.00
```

## EXPLANATION

+   1 The local variable name is assigned the value Bob. The double quotes allow the dollar sign to be used for variable substitution.
+   2 The single quote is protected within double quotes.
