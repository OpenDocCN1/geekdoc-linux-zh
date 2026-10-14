```
name[subscript]=value
```

where name is the name of the array and subscript is an integer (or arithmetic expression) greater than or equal to zero. Note that an array’s first element is subscript zero, not one. value is a string or integer assigned to the array element.

Multiple values may be assigned using the following syntax:

```
name=(value1 value2 ...)
```

where name is the name of the array and the value placeholders are values assigned sequentially to elements of the array, starting with element zero. For example, if we wanted to assign abbreviated days of the week to the array days, we could do this:

```
[me@linuxbox ~]$ days=(Sun Mon Tue Wed Thu Fri Sat)
```

It is also possible to assign values to a specific element by specifying a subscript for each value.

```
[me@linuxbox ~]$ days=([0]=Sun [1]=Mon [2]=Tue [3]=Wed [4]=Thu [5]=Fri [6]=Sat)
```

# Accessing Array Elements

So, what are arrays good for? Just as many data-management tasks can be performed with a spreadsheet program, many programming tasks can be performed with arrays.

Let’s consider a simple data-gathering and presentation example. We will construct a script that examines the modification times of the files in a specified directory. From this data, our script will output a table showing at what hour of the day the files were last modified. Such a script could be used to determine when a system is most active. This script, called hours, produces this result: