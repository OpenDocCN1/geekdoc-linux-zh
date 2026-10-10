# ## Using Variables in Functions

You might have noticed in the `test5` example in the previous section that I used a variable called `$value` within the function to hold the value that it processed. When you use variables in your functions, you need to be somewhat careful about how you define and handle them. This is a common cause of problems in shell scripts. This section goes over a few techniques for handling variables, both inside and outside your shell script functions.

# ### Passing parameters to a function

As mentioned earlier in the “Returning a Value from a Function” section, the Bash shell treats functions just like mini-scripts. This means that you can pass parameters to a function just like a regular script (see Chapter 14, “Handling User Input”).

Functions can use the standard parameter environment variables to represent any parameters passed to the function on the command line. For example, the name of the function is defined in the `$0` variable, and any parameters on the function command line are defined using the variables `$1`, `$2`, and so on. You can also use the special variable `$#` to determine the number of parameters passed to the function.

When specifying the function in your script, you must provide the parameters on the same command line as the function, like this:

```
`func1 $value1 10`
```

The function can then retrieve the parameter values using the parameter environment variables. Here’s an example of using this method to pass values to a function:

```
```
$ cat test6
#!/bin/bash
# passing parameters to a function

function addem {
    if [ $# -eq 0 ] || [ $# -gt 2 ]
    then
        echo -1
    elif [ $# -eq 1 ]
    then
        echo ${$1 + $1}
    else
        echo ${$1 + $2}
    fi
}

echo -n "Adding 10 and 15: "
value=$(addem 10 15)
echo $value
```
```