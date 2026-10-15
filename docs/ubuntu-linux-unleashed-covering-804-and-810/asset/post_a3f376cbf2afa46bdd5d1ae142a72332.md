
## TABLE 11.2 Special Shell Characters

| Character | Explanation |
| --- | --- |
| $ | Indicates the beginning of a shell variable name |
| | | Pipes standard output to next command |
| # | Starts a comment |
| & | Executes a process in the background |
| ? | Matches one character |
| * | Matches one or more characters |
| > | Output redirection operator |
| < | Input redirection operator |
| ` | Command substitution (the backquote or backtick—the key above the Tab key on most keyboards) |
| >> | Output redirection operator (to append to a file) |
| << | Wait until following end-of-input string (HERE operator) |
| [ ] | Range of characters |
| [a-z] | All characters a through z |
| [a,z] or [az] | Characters a or z |
| Space | Delimiter between two words |

Special characters are very useful to you when you're creating shell scripts, but if you inadvertently use a special character as part of variable names or strings, your program will behave incorrectly. As you learn in later parts of this section, you can use one of the special characters in a string if you precede it with an escape character (\), or backslash) to indicate that it isn't being used as a special character and shouldn't be treated as such by the program.

A few special characters deserve special note. They are the double quotes ("), the single quotes ('), the backslash (\), and the backtick (`)—all discussed in the following sections.

## Use Double Quotes to Resolve Variables in Strings with Embedded Spaces

If a string contains embedded spaces, you can enclose the string in double quotes (") so that the shell interprets the whole string as one entity instead of more than one.

For example, if you assigned the value of abc def (abc followed by one space, followed by def) to a variable called x in a shell program as follows, you would get an error because the shell would try to execute def as a separate command:

| Command | Environment |
|---|---|
| x="abc def" | pdksh and bash |
| set x = "adb def" | tcsh |

The shell will execute the string as a single command if you surround the string in double quotes as follows:

| Command | Environment |
|---|---|
| x=abc def | pdksh and bash |
| set x=abc def | tcsh |

The double quotes resolve all variables within the string. Here is an example for pdksh and bash:

```
var="test string"
newvar="Value of var is $var"
echo $newvar
```

Here is the same example for tcsh:

```
set var="test string"
set newvar="Value of var is $var"
echo $newvar
```

If you execute a shell program containing the preceding three lines, you get the following result:

Value of var is test string

## Using Single Quotes to Maintain Unexpanded Variables

You can surround a string with single quotes (') to stop the shell from expanding variables and interpreting special characters. When used for the latter purpose, the single quote is an escape character, similar to the backslash, which you learn about in the next section. Here, you learn how to use the single quote to avoid expanding a variable in a shell script. An unexpanded variable maintains its original form in the output.

![](img/8f9e74e2b343ff525bebfb720a3d8441_296_0.png)

FIGURE 14.5 Keep the speaker volume turned down low otherwise you'll hear incessant screeching during the dial-up process.

Make sure to enter your ISP's phone number as well as your username and password; essential information if you are to succeed at getting on to the Internet!

![](img/8f9e74e2b343ff525bebfb720a3d8441_296_1.png)

FIGURE 14.6 A couple of choices here will ensure uninterrupted surfing time.

```
if [ $string1 = $string2 ]; then
  echo 'string1 equal to string2'
else
  echo 'string1 not equal to string2'
fi
```

```
if [ $string2 != string1 ]; then
  echo 'string2 not equal to string1'
else
  echo 'string2 equal to string2'
fi
```

```
if [ $string1 ]; then
  echo 'string1 is not empty'
else
  echo 'string1 is empty'
fi
```

```
if [ -n $string2 ]; then
  echo 'string2 has a length greater than zero'
else
  echo 'string2 has length equal to zero'
fi
```

```
if [ -z $string1 ]; then
  echo 'string1 has a length equal to zero'
else
  echo 'string1 has a length greater than zero'
fi
```

If you execute compare1, you get the following result:

```
string1 not equal to string2
string2 not equal to string1
string1 is not empty
string2 has a length greater than zero
string1 has a length greater than zero
```

If two strings are not equal in size, the system pads out the shorter string with trailing spaces for comparison. That is, if the value of string1 is abc and that of string2 is ab, string2 will be padded with a trailing space for comparison purposes—it will have a value of ab.

## Number Comparison

The following operators can be used to compare two numbers:

- -eq—To compare whether two numbers are equal
- -ge—To compare whether one number is greater than or equal to the other number
- -le—To compare whether one number is less than or equal to the other number
