Shall we try adding a single number: 20

I am not trying to add any numbers now: -1

Finally, I am trying to add three numbers: -1

The addmedigits function checks the number of parameters that are passed to the function. If there are no parameters or more than two parameters, the value is returned as -1. If there is a single parameter, it adds that to itself for the result. If there are two parameters, it adds all of them for the result. Since the function uses a special parameter environment variable for its parameter values, it cannot access the script parameter values from the command line of the script.

# **Passing Arrays to Functions**

Passing arrays into functions is a precise art but, to start with, it may be confusing. If an array variable is passed as a single variable, it will not work:

```
```
$ cat badtest3
#!/bin/bash
function func555 {
echo "The parameters being used in the function are: $@"
myarray=$1
echo "The array that is received is as follows: ${myarray[*]}"
thisarray=(1 2 3 4 5 6 7 8 9 10)
echo "This is the original array : ${thisarray[*]}"
func555 $thisarray
$bash -f main.sh
```
```

This is the original array : 1 2 3 4 5 6 7 8 9 10

The parameters being used in the function are: 1

The array that is received is as follows: 1

If you try to use the array variable as a function parameter, the function takes the first value in the array variable. Fixing this requires that the array variable is broken down into its individual values, which are then used as function parameters. You can reassemble those parameters in the function as a new array variable. Here’s an example:

```
```
$ cat test10
#!/bin/bash
function testingfunction {
```
```