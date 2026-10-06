```
function dbl {
  value=$[ value * 2 ]
}
```

```
read -p "Enter a value: " value dbl
echo "The new value is: $value"
$ ./test8
Enter a value: 450
The new value is: 900
$
```

The $value variable is defined outside of the function, and assigned a value outside of the function. When the dbl function is called, the variable and its value are still valid inside the function. When the variable is assigned a new value inside the function, that new value is still valid when the script references the variable.

This can be a dangerous practice, especially if you intend to use your functions in different shell scripts. It requires that you know exactly what variables are used in the function, including any variables used to calculate values not returned to the script. Here's an example of how things can go:

```
$ cat badtest2
#!/bin/bash
# demonstrating a bad use of variables
```

```
function func1 {
  temp=$[ value + 5 ]
  result=$[ temp * 2 ]
}
```

```
temp=4
value=6
```

```
func1
echo "The result is $result"
if [ $temp -gt $value ]
then
  echo "temp is larger"
else
  echo "temp is smaller"
fi
$ ./badtest2
The result is 22
temp is larger
$
```

The $temp variable was used in the function, its value is compromised in the script, producing a result that you may not have intended. There's an easy way to solve this problem in your functions, shown in the next section.