
```sh
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

If two strings are not equal in size, the system pads out the shorter string with trailing spaces for comparison. That is, if the value of string1 is abc and that of string2 is ab, string2 will be padded with a trailing space for comparison purposes—it will have a value of "ab " (represented as ab in the text).

## Number Comparison

The following operators can be used to compare two numbers:

- `-eq`—To compare whether two numbers are equal
- `-ge`—To compare whether one number is greater than or equal to the other number
- `-le`—To compare whether one number is less than or equal to the other number
- `-ne`—To compare whether two numbers are not equal
- `-gt`—To compare whether one number is greater than the other number
- `-lt`—To compare whether one number is less than the other number

The following shell program compares three numbers, number1, number2, and number3:

```bash
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

When you execute the shell program, you get the following results:

number1 is equal to number3
number1 is not equal to number2
number1 is not greater than number2
number1 is greater than or equal to number3
number1 is less than number2
number1 is less than or equal to number3

## File Operators

The following operators can be used as file comparison operators:

- `-d`—To ascertain whether a file is a directory
- `-f`—To ascertain whether a file is a regular file
- `-r`—To ascertain whether read permission is set for a file
- `-s`—To ascertain whether a file exists and has a length greater than zero
- `-w`—To ascertain whether write permission is set for a file
- `-x`—To ascertain whether execute permission is set for a file

Assume that a shell program called compare3 is in a directory with a file called file1 and a subdirectory dir1 under the current directory. Assume that file1 has a permission of r-x (read and execute permission) and dir1 has a permission of rwx (read, write, and execute permission). The code for the shell program would look like this:

```sh
#!/bin/sh
if [ -d $dir1 ]; then
    echo "$dir1 is a directory"
else
    echo "$dir1 is not a directory"
fi

if [ -f $dir1 ]; then
    echo "$dir1 is a regular file"
else
    echo "$dir1 is not a regular file"
fi

if [ -r $file1 ]; then
    echo "$file1 has read permission"
else
    echo "$file1 does not have read permission"
fi

if [ -w $file1 ]; then
  echo "$file1 has write permission"
else
  echo "$file1 does not have write permission"
fi

if [ -x $dir1 ]; then
  echo "$dir1 has execute permission"
else
  echo "$dir1 does not have execute permission"
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

- `!`—To negate a logical expression
- `-a`—To logically AND two logical expressions
- `-o`—To logically OR two logical expressions

This example named `logic` uses the file and directory mentioned in the previous `compare3` example.

```sh
#!/bin/sh
if [ -x file1 -a -x dir1 ]; then
  echo "file1 and dir1 are executable"
else
  echo "at least one of file1 or dir1 are not executable"
fi

if [ -w file1 -o -w dir1 ]; then
  echo "file1 or dir1 are writable"
else
  echo "neither file1 or dir1 are writable"
fi

if [ ! -w file1 ]; then
  echo "file1 is not writable"
else
  echo "file1 is writable"
fi
```

If you execute `logic`, it yields the following result:

file1 and dir1 are executable
file1 or dir1 are writable
file1 is not writable

## Comparing Expressions with tcsh

As stated earlier, the method for comparing expressions in tcsh is different from the method used under dash and bash. The comparison of expressions demonstrated in this section uses the syntax necessary for the tcsh shell environment.

### String Comparison

The following operators can be used to compare two string expressions:

- `==`—To compare whether two strings are equal
- `!=`—To compare whether two strings are not equal

The following examples compare two strings, string1 and string2, in the shell program compare1:

```csh
#!/bin/tcsh
set string1 = "abc"
set string2 = "abd"

if (string1 == string2) then
  echo "string1 equal to string2"
else
  echo "string1 not equal to string2"
endif

if (string2 != string1) then
  echo "string2 not equal to string1"
else
  echo "string2 equal to string1"
endif
```

If you execute compare1, you get the following results:

string1 not equal to string2
string2 not equal to string1

### Number Comparison

These operators can be used to compare two numbers:

- `>=`—To compare whether one number is greater than or equal to the other number
- `<=`—To compare whether one number is less than or equal to the other number
- `>`—To compare whether one number is greater than the other number
- `<`—To compare whether one number is less than the other number

The next examples compare two numbers, *number1* and *number2*, in a shell program called compare2:

```csh
#!/bin/tcsh
set number1=5
set number2=10
set number3=5

if ($number1 > $number2) then
    echo "number1 is greater than number2"
else
    echo "number1 is not greater than number2"
endif

if ($number1 >= $number3) then
    echo "number1 is greater than or equal to number3"
else
    echo "number1 is not greater than or equal to number3"
endif

if ($number1 < $number2) then
    echo "number1 is less than number2"
else
    echo "number1 is not less than number2"
endif

if ($number1 <= $number3) then
    echo "number1 is less than or equal to number3"
else
    echo "number1 is not less than or equal to number3"
endif
```

When executing the shell program *compare2*, you get the following results:

number1 is not greater than number2
number1 is greater than or equal to number3
number1 is less than number2
number1 is less than or equal to number3

![](img/2045828cf45e5632bf056f9ca99d6755_432_0.png)

## File Operators

These operators can be used as file comparison operators:

- `-d`—To ascertain whether a file is a directory
- `-e`—To ascertain whether a file exists
- `-f`—To ascertain whether a file is a regular file
- `-o`—To ascertain whether a user is the owner of a file
- `-r`—To ascertain whether read permission is set for a file
- `-w`—To ascertain whether write permission is set for a file
- `-x`—To ascertain whether execute permission is set for a file
- `-z`—To ascertain whether the file size is zero

The following examples are based on a shell program called `compare3`, which is in a directory with a file called `file1` and a subdirectory `dir1` under the current directory. Assume that `file1` has a permission of `r-x` (read and execute permission) and `dir1` has a permission of `rwx` (read, write, and execute permission).

The following is the code for the `compare3` shell program:

```csh
#!/bin/csh
if (-d dir1) then
    echo "dir1 is a directory"
else
    echo "dir1 is not a directory"
endif

if (-f dir1) then
    echo "file1 is a regular file"
else
    echo "file1 is not a regular file"
endif

if (-r file1) then
    echo "file1 has read permission"
else
    echo "file1 does not have read permission"
endif

if (-w file1) then
    echo "file1 has write permission"
else
    echo "file1 does not have write permission"
endif
```
