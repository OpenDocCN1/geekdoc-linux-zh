
you get the following result:

```
Number of parameters is 2
Program name is myprog2
Parameters as a single string is Sanjiv Guha
```

## Special Characters

Some characters have special meaning to Linux shells, so using them as part of variable names or strings causes your program to behave incorrectly. If a string contains such characters, you also have to use escape characters (backslashes) to indicate that the special characters should not be treated as special characters. Some of these characters are shown in Table 25.2.

**TABLE 25.2 Special Shell Characters**

| Character | Explanation |
| :--- | :--- |
| $ | Indicates the beginning of a shell variable name |
| \| | Pipes standard output to next command |
| # | Starts a comment |
| & | Executes a process in the background |
| ? | Matches one character |
| * | Matches one or more characters |
| > | Output redirection operator |
| < | Input redirection operator |
| ` | Command substitution (the backquote or backtick—the key above the Tab key on most keyboards) |
| >> | Output redirection operator (to append to a file) |
| << | Wait until following end-of-input string (`HERE` operator) |
| [ ] | Lists a range of characters |
| [a-z] | All characters a through z |
| [a,z] | Characters a or z |
| . `filename` | Executes (“sources”) the file `filename` |
| Space | Delimiter between two words |

A few characters deserve special note. They are the double quotes (`"`), the single quotes (`'`), the backslash (`\`), and the backtick (`` ` ``), all discussed in the following sections. Also note that you can use input and output redirection from inside your shell scripts. Be sure to use output redirection with care when you're testing your shell programs, because you can easily overwrite files!

## Double Quotes

If a string contains embedded spaces, you can enclose the string in double quotes (`"`) so the shell interprets the whole string as one entity instead of more than one. For example, if you assigned the value of abc_def (abc followed by one space followed by def) to a variable called x in a shell program as follows, you would get an error because the shell would try to execute def as a separate command.

| Command | Environment |
| --- | --- |
| x=abc def | pdksh and bash |
| set x = abc def | tcsh |

What you need to do is surround the string in double quotes:

| Command | Environment |
| --- | --- |
| x="abc def" | pdksh and bash |
| set x = "abc def" | tcsh |

The double quotes resolve all variables within the string. Here is an example for pdksh and bash:

```
var="test string" 
newvar="Value of var is $var" 
echo $newvar
```

Here is the same example for tcsh:

```
set var = "test string" 
set newvar = 'Value of var is $var' 
echo $newvar
```

If you execute a shell program containing these three lines, you get the following result:

Value of var is test string

## Single Quotes

You can surround a string with single quotes (`'`) to stop the shell from resolving a variable. In the following examples, the double quotes in the preceding examples have been changed to single quotes.

pdksh and bash:

```
var='test string' 
newvar='Value of var is $var' 
echo $newvar
```

tcsh:

```
set var = 'test string'
set newvar = 'Value of var is $var'
echo $newvar
```

If you execute a shell program containing these three lines, you get the following result:

Value of var is $var

As you can see, the variable var did not get interpolated.

## Backslash

You can use a backslash (`\`) before a character to stop the shell from interpreting the succeeding character as a special character. Say you want to assign a value of $test to a variable called var. If you use the following command, a null value is stored in var:

| Command | Environment |
| --- | --- |
| var=$test | pdksh and bash |
| set var = $test | tcsh |

This happens because the shell interprets $test as the value of the variable test. No value has been assigned to test, so var contains null. You should use the following command to correctly store $test in var:

| Command | Environment |
| --- | --- |
| var=\$test | pdksh and bash |
| set var = \$test | tcsh |

The backslash (`\`) before the dollar sign (`$`) signals the shell to interpret the $ as any other ordinary character and not to associate any special meaning to it.

## Backtick

You can use the backtick (`` ` ``) character to signal the shell to execute the string delimited by the backtick. This can be used in shell programs when you want the result of execution of a command to be stored in a variable. For example, if you want to count the number of lines in a file called test.txt in the current directory and store the result in a variable called var, you can use the following command:

| Command | Environment |
| --- | --- |
| var=`wc -l test.txt` | pdksh and bash |
| set var = `wc -l test.txt` | tcsh |

# PART IV

## Comparison of Expressions

The way the logical comparison of two operators (numeric or string) is done varies slightly in different shells. In `pdksh` and `bash`, a command called **test** can be used to achieve comparisons of expressions. In `tcsh`, you can write an expression to accomplish the same thing.

### `pdksh` and `bash`

This section covers comparisons using the `pdksh` or `bash` shells. Later in the chapter, the section **“tcsh”** contains a similar discussion for the `tcsh` shell.

The syntax of the **test** command is as follows:

```
test expression
or
[ expression ]
```

Both forms of **test** commands are processed the same way by `pdksh` and `bash`. The **test** commands support the following types of comparisons:

- String comparison
- Numeric comparison
- File operators
- Logical operators

### String Comparison

The following operators can be used to compare two string expressions:

| Operator | Description |
| -------- | ----------- |
| `=` | To compare whether two strings are equal |
| `!=` | To compare whether two strings are not equal |
| `-n` | To evaluate whether the string length is greater than zero |
| `-z` | To evaluate whether the string length is equal to zero |

Next are some examples comparing two strings, `string1` and `string2`, in a shell program called **compare1**:

```shell
#!/bin/sh
string1="abc"
string2="abd"
if [ $string1 = $string2 ]; then
    echo "string1 equal to string2"
else
    echo "string1 not equal to string2"
fi

if [ $string2 != string1 ]; then
    echo "string2 not equal to string1"
else
    echo "string2 equal to string2"
fi

if [ $string1 ]; then
    echo "string1 is not empty"
else
    echo "string1 is empty"
fi

if [ -n $string2 ]; then
    echo "string2 has a length greater than zero"
else
    echo "string2 has length equal to zero"
fi

if [ -z $string1 ]; then
    echo "string1 has a length equal to zero"
else
    echo "string1 has a length greater than zero"
fi
```

If you execute compare1, you get the following result:

string1 not equal to string2
string2 not equal to string1
string1 is not empty
string2 has a length greater than zero
string1 has a length greater than zero

If two strings are not equal in size, the system pads out the shorter string with trailing spaces for comparison. That is, if the value of string1 is abc and that of string2 is ab, string2 will be padded with a trailing space for comparison purposes—it will have a value of ab .

### Number Comparison

The following operators can be used to compare two numbers:

- -eq To compare whether two numbers are equal
- -ge To compare whether one number is greater than or equal to the other number
- -le To compare whether one number is less than or equal to the other number
- -ne To compare whether two numbers are not equal
- -gt To compare whether one number is greater than the other number
- -lt To compare whether one number is less than the other number

The following examples compare two numbers, number1 and number2, in a shell program called compare2:

```
#!/bin/sh
number1=5
number2=10
number3=5

if [ $number1 -eq $number3 ]; then
    echo "number1 is equal to number3"
else
    echo "number1 is not equal to number3"
fi

if [ $number1 -ne $number2 ]; then
    echo "number1 is not equal to number2"
else
    echo "number1 is equal to number2"
fi

if [ $number1 -gt $number2 ]; then
    echo "number1 is greater than number2"
else
    echo "number1 is not greater than number2"
fi

if [ $number1 -ge $number3 ]; then
    echo "number1 is greater than or equal to number3"
else
    echo "number1 is not greater than or equal to number3"
fi

if [ $number1 -lt $number2 ]; then
    echo "number1 is less than number2"
else
    echo "number1 is not less than number2"
fi

if [ $number1 -le $number3 ]; then
    echo "number1 is less than or equal to number3"
else
    echo "number1 is not less than or equal to number3"
fi
```

When you execute the shell program compare2, you get the following results:

```
number1 is equal to number3
number1 is not equal to number2
number1 is not equal to number2
number1 is greater than or equal to number3
number1 is less than number2
number1 is less than or equal to number3
```
