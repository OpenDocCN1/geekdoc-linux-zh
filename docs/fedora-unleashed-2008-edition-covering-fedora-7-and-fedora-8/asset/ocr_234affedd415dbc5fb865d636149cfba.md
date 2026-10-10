If two strings are not equal in size, the system pads out the shorter string with trailing spaces for comparison. That is, if the value of `string1` is ab and that of `string2` is ab, `string2` will be padded with a trailing space for comparison purposes—it will have a value of ab.

# Number Comparison

The following operators can be used to compare two numbers:

+   - `-eq`—To compare whether two numbers are equal
+   - `-ge`—To compare whether one number is greater than or equal to the other number
+   - `-le`—To compare whether one number is less than or equal to the other number
+   - `-ne`—To compare whether two numbers are not equal
+   - `-gt`—To compare whether one number is greater than the other number
+   - `-lt`—To compare whether one number is less than the other number

The following shell program compares three numbers, `number1`, `number2`, and `number3`:

```
```sh
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
```
```