Now when you use the *$temp* variable within the *func1* function, it doesn't affect the value assigned to the *$temp* variable in the main script.

# # Investigating Array Variables and Functions

Chapter 5, “Understanding the Shell,” discussed an advanced way of allowing a single variable to hold multiple values by using arrays. Using array variable values with functions is a little tricky, and there are some special considerations. This section describes a technique that allows you to use array variable values with functions.

# ## Passing arrays to functions

The art of passing an array variable to a script function can be confusing. If you try to pass the array variable as a single parameter, it doesn't work:

```
```
$ cat badtest3
#!/bin/bash
# trying to pass an array variable

function testit {
    echo "The parameters are: $@"
    thisarray=$1
    echo "The received array is ${thisarray[*]}"
}
myarray=(1 2 3 4 5)
echo "The original array is: ${myarray[*]}"
testit $myarray
$
$ ./badtest3
The original array is: 1 2 3 4 5
The parameters are: 1
The received array is 1
$ 
```
```

If you try using the array variable as a function parameter, the function picks up only the first value of the array variable.

To solve this problem, you must disassemble the array variable into its individual values and use the values as function parameters. Inside the function, you can reassemble all the parameters into a new array variable. Here's an example of doing this:

```
```
$ cat test10
#!/bin/bash
# array variable to function test

function testit {
    local newarray
    newarray=("echo "$@"")
    echo "The new array value is: ${newarray[*]}"
}
```
```