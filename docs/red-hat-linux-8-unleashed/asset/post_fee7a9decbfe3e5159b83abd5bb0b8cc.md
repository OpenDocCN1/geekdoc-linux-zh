
# Comparison of Expressions

varies slightly in different shells. In pdsh and bash, a command called test can be used to achieve comparisons of expressions. In tsh, you can write an expression to accomplish the same thing.

The following section covers comparison operations using the pdsh or bash shells. Later in the chapter, you learn how to compare expressions in the tsh shell.

# Comparison of Expressions in pdsh and bash

The pdsh and bash shell syntax provide a command named test to compare strings, numbers, and files. The syntax of the test command is as follows

```
expression
```

or

```
[ expression ]
```

Both forms of test commands are processed the same way by pdsh and bash. The test commands support the following types of comparisons:

- String comparison
- Numeric comparison
- File operators
- Logical operators

## String Comparison

The following operators can be used to compare two expressions:

- = To compare whether two strings are equal
- != To compare whether two strings are not equal
- -n To evaluate whether the string length is greater than zero
- -z To evaluate whether the string length is equal to zero

Next are some examples using these operators when comparing two strings, string1 and string2, in a shell program called compare:

```
#!/bin/sh
string1="abc"
string2="abd"
if [ $string1 = $string2 ]; then
  echo "string1 equal to string2"
else
  echo "string1 not equal to string2"
fi

if [ $string2 != $string1 ]; then
  echo "string2 not equal to string1"
else
  echo "string2 equal to string2"
fi

if [ -n $string1 ]; then
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
  echo "string1 has length equal to zero"
else
  echo "string1 has a length greater than zero"
fi
```

If you execute compare, you get the following result:
string1 not equal to string2
string2 not equal to string1
string1 is not empty
string2 has a length greater than zero

## Number Comparison

The following operators can be used to compare two numbers:

- -eq To compare whether two numbers are equal
- -ge To compare whether one number is greater or equal to the other
- -le To compare whether one number is less or equal to the other
- -ne To compare whether two numbers are not equal
- -gt To compare whether one number is greater than the other
- -lt To compare whether one number is less than the other

The following shell program compares three numbers, number1, number2, and number3:

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
    echo "number1 is greater or equal to number3"
else
    echo "number1 is not greater or equal to number3"
fi

if [ $number1 -lt $number2 ]; then
    echo "number1 is less than number2"
else
    echo "number1 is not less than number2"
fi

if [ $number1 -le $number3 ]; then
    echo "number1 is less or equal to number3"
else
    echo "number1 is not less or equal to number3"
fi
```

## File Operators

The following operators can be used as file comparison:

- -d To ascertain whether a file is a directory
- -f To ascertain whether a file is a regular file
- -r To ascertain whether read permission is set for a file
- -s To ascertain whether a file exists and has a length greater than zero
- -w To ascertain whether write permission is set for a file
- -x To ascertain whether execute permission is set for a file

Assume that a shell program called compare is in a directory with a file called file1 and a subdirectory dir1 under the current directory. Assume that file1 has a permission of rx (read and execute permission) and dir1 has a permission of rwx (read, write, and execute permission). The code for the shell program would look like this:

```
#!/bin/sh
if [ -d $dir1 ]; then
  echo "dir1 is a directory"
else
  echo "dir1 is not a directory"
fi

if [ -f $file1 ]; then
  echo "file1 is a regular file"
else
  echo "file1 is not a regular file"
fi

if [ -r $file1 ]; then
  echo "file1 has read permission"
else
  echo "file1 does not have read permission"
fi

if [ -w $file1 ]; then
  echo "file1 has write permission"
else
  echo "file1 does not have write permission"
fi

if [ -x $dir1 ]; then
  echo "dir1 has execute permission"
else
  echo "dir1 does not have execute permission"
fi
```

If you execute the shell program, you get the following results:
dir1 is a directory
file1 is a regular file
file1 has read permission
file1 does not have write permission
dir1 has execute permission

## Logical Operators

Logical operators are used to compare expressions using Boolean logic, which compares values using characters representing NOT, AND, and OR.

- ! To negate a logical expression
- a To logically AND two logical expressions
- o To logically OR two logical expressions

This example named logic uses the file and directory mentioned in the previous compare example.

```
#!/bin/sh
if [ -x file1 -a -x dir1 ]; then
    echo "file1 and dir1 are executable"
else
    echo "at least one of file1 or dir1 are not executable"
fi

if [ -w file1 -o -w dir1 ]; then
    echo "file1 or dir1 are writable"
else
    echo "neither file1 or dir1 are executable"
fi

if [ ! -w file1 ]; then
    echo "file1 is not writable"
else
    echo "file1 is writable"
fi
```

If you execute logic, it will yield the following result:
file1 and dir1 are executable
file1 or dir1 are writable
file1 is not writable

# Comparing Expressions with tcsh

As stated earlier, the method for comparing expressions in tcsh is different from the method used under pdsh and bash. The comparison of expression demonstrated in this section uses the syntax necessary for the tcsh shell environment.

## String Comparison

The following operators can be used to compare two string expressions:

- == To compare whether two strings are equal
- != To compare whether two strings are not equal

The following examples compare two strings, string1 and string2, in the shell program compare1:

```tcsh
#!/bin/tcsh
set string1 = "abc"
set string2 = "abd"

if ($string1 == string2) then
    echo "string1 equal to string2"
else
    echo "string1 not equal to string2"
endif

if ($string2 != string1) then
    echo "string2 not equal to string1"
else
    echo "string2 equal to string1"
endif
```

If you execute compare1, you get the following results:
string1 not equal to string2
string2 not equal to string1

## Number Comparison

These operators can be used to compare two numbers:

- == To compare whether one number is greater than or equal to the other
- <= To compare whether one number is less or equal to the other
- > To compare whether one number is greater than the other
- < To compare whether one number is less than the other
