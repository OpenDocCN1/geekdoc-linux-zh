# Associative Arrays

An associative array is one of gawk's most powerful features. An associative array uses strings as its indices. Using an associative array, you can mimic a traditional array by numeric strings as indexes.

You assign a value to an element of an associative array just as you assign a value to any other gawk variable. The syntax is

```
array[string] = value
```

The array is the name of the array, string is the index of the element of the array you are assigning a value to, and value is the value you are assigning to the element of the array.

You can use a special for structure with a gawk array. The syntax is

```
for (elem in array) action
```

The elem is a variable that takes on the values of each of the elements in the array as for structure loops through them, array is the name of the array, and actions is the action that gawk takes for each element in the array. You can use the elem variable in this action.

The "Examples" section contains programs that use associative arrays.

# printf

You can use the printf command in place of print to control the format of the output that gawk generates. The gawk version of printf is similar to that of the C language. A printf command takes the following syntax:

```
printf "control-string", arg1, arg2, ..., argn
```

The control-string determines how printf formats arg1-n. The arg1-n can be variables or other expressions. Within the control you can use \n to indicate a NEWLINE and \t to indicate a TAB.

The control-string contains conversion specifications, one for each argument (arg1n). A conversion specification has the following syntax:

```
%-%[x.]conv
```

The causes printf to left justify the argument. The x is the minimum field width, and the .y is the number of places to the right of a decimal point in a number. The conv is a letter from the list in Table III-17.

Refer to the following "Examples" section for examples of how to use printf.