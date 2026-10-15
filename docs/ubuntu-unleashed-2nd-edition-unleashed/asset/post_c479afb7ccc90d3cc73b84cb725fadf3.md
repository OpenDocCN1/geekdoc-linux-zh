
## Number Comparison

The following operators can be used to compare two numbers:

- -eq—To compare whether two numbers are equal
- -ge—To compare whether one number is greater than or equal to the other number
- -le—To compare whether one number is less than or equal to the other number
- -ne—To compare whether two numbers are not equal
- -gt—To compare whether one number is greater than the other number
- -lt—To compare whether one number is less than the other number

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
    echo "number1 is greater than or equal to number3"
else
    echo "number1 is not greater than or equal to number3"
fi

if [ $number1 -lt $number2 ]; then
    echo "number1 is less than number2"
else
    echo 'number1 is not less than number2'
fi
```

```
if [ $number1 -le $number3 ]; then
    echo 'number1 is less than or equal to number3'
else
    echo 'number1 is not less than or equal to number3'
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

- -d—To ascertain whether a file is a directory
- -f—To ascertain whether a file is a regular file
- -r—To ascertain whether read permission is set for a file
- -s—To ascertain whether a file exists and has a length greater than zero
- -w—To ascertain whether write permission is set for a file
- -x—To ascertain whether execute permission is set for a file

Assume that a shell program called compare3 is in a directory with a file called file1 and a subdirectory dir1 under the current directory. Assume that file1 has a permission of r-x (read and execute permission) and dir1 has a permission of rwx (read, write, and execute permission). The code for the shell program would look like this:

```
#!/bin/sh
if [ -d $dir1 ]; then
    echo "dir1 is a directory"
else
    echo "dir1 is not a directory"
fi
```

```
if [ -f $dir1 ]; then
    echo "dir1 is a regular file"
```

```
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

```
string1 not equal to string2
string2 not equal to string1
```

## Number Comparison

These operators can be used to compare two numbers:

- `>=` To compare whether one number is greater than or equal to the other number
- `<=` To compare whether one number is less than or equal to the other number
- `>` To compare whether one number is greater than the other number
- `<` To compare whether one number is less than the other number

The next examples compare two numbers, number1 and number2, in a shell program called compare2:

```
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
```
