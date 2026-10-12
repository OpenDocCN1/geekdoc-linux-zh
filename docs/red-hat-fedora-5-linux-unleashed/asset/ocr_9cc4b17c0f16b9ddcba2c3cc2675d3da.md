The following section covers comparison operations using the pdksh or bash shells. Later in the chapter, you learn how to compare expressions in the tcsh shell.
The pdksh and bash shell syntax provide a command named **test** to compare strings, numbers, and files. The syntax of the **test** command is as follows:
**test** *expression*
or
[ *expression* ]
Both forms of the **test** commands are processed the same way by pdksh and bash. The **test** commands support the following types of comparisons:

+   - String comparison
+   - Numeric comparison
+   - File operators
+   - Logical operators

# String Comparison

The following operators can be used to compare two string expressions:

+   —To compare whether two strings are equal
+   !=—To compare whether two strings are not equal
+   -n—To evaluate whether the string length is greater than zero
+   -z—To evaluate whether the string length is equal to zero

Next are some examples using these operators when comparing two strings, *string1* and *string2*, in a shell program called *compare1*:

```
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
```