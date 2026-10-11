The first parameter is a format string describing how the items being printed will be represented. For example, the special formatting code `*$d*` represents an integer number, and the code `*$f*` represents a floating-point number.

```
$ printf "*$d*\n" 5
5
$ printf "*$f*\n" 5
5.000000
```

Include a format code for each item you want to print. Each format code is replaced with the appropriate value when printed. Any characters in the format string that are not part of a formatting instruction are treated as printable characters.

```
$ printf "There are *%d* customers with purchases over *%d*.\n" 50 20000
There are 50 customers with purchases over 20000.
```

printf is sometimes used to redirect a variable or some unchanging input to a command. For example, suppose all you want to do is pipe a variable to a command. Instead of using printf, Bash provides a shortcut << redirection operator. << redirects a string into a command as if it were piped using printf.

The tr command can convert text to uppercase. This example shows an error message being converted to uppercase with both printf and <<.

```
$ printf "*$a*\n" "$ERRMSG" | tr [[:lower:]] [[:upper:]]
WARNING: THE FILES FROM THE OHIO OFFICE HAVEN'T ARRIVED.
$ tr [[:lower:]] << [[:upper:]] << "$ERRMSG"
WARNING: THE FILES FROM THE OHIO OFFICE HAVEN'T ARRIVED.
```

The format codes include the following.

+   * *%a*—Represent a floating-point number in hexadecimal format, using lowercase letters
+   * *%A*—Represent a floating point number in hexadecimal format, using uppercase letters
+   * *%b*—Expand backslash sequences
+   * *%c*—Represent a single character
+   * *%d*—Display a signed number
+   * *%e*—Display a floating-point number, shown in exponential (also called “scientific”) notation
+   * *%f* (or *%F*)—Display a floating-point number without exponential notation
+   * *%g*—(General) Let Bash choose *%e* or *%f*, depending on the value
+   * *%i*—Same as *%d*
+   * *%o*—Display an octal number
+   * *%q*—Quote a string so it can be read properly by a shell script