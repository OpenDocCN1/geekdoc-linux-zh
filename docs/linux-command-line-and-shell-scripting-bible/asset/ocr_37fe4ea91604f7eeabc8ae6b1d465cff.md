# Part III Advanced Shell Scripting

```
newarray=`echo "$@'
echo "The new array value is: ${newarray[*]}

```

```
myarray=(1 2 3 4 5)
echo "The original array is ${myarray[*]}
testit $[myarray[*]}
$ ./test10
The original array is 1 2 3 4 5
The new array value is: 1 2 3 4 5
$
```

The script uses $myarray variable to hold all of the individual array values to place them all on the command line for the function. The function then rebuilds the array variable from the command line parameters. Once the function, the array can be rebuilt just like any other array:

```
$ cat test1
#!/bin/bash
# adding values in an array
```

```
function addarray (
  local sum=0
  local newarray=`echo "$@'
  for value in ${newarray[*]}
do
    sum=$[$sum + $value]
done
  echo $sum

```

```
myarray=(1 2 3 4 5)
echo "The original array is: ${myarray[*]}
arg1=`echo ${myarray[*]}
result=`addarray $arg1
echo "The result is $result"
$ ./test1
The original array is: 1 2 3 4 5
The result is 15
$
```

The addarray function iterates through the array values, adding them together. You can put any number of values in the myarray array variable, and the addarray function will add them.

# Returning arrays from functions

Passing an array variable from a function back to the shell script uses a similar technique. The function uses an echo statement to output the individual array values in the proper order, then

376