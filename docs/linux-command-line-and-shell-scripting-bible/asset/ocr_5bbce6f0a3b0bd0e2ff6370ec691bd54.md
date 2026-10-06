# Part III Advanced Shell Scripting

common cause of problems in shell scripts. This section goes over a few techniques for handling variables both inside and outside your shell functions.

# Passing parameters to a function

As was mentioned earlier in the “Returning a Value” section, the bash shell treats functions just like mini-scripts. This means you can pass parameters to a function just like a regular script (see Chapter 11).

Functions use the standard parameter environment variables to represent any parameters passed to the function on the command line. For example, the name of the function is defined in the $0 variable, and any parameters on the function command line are defined using the $1, $2, and so on. You can also use the special variable $$ to determine the number of parameters passed to the function.

When specifying the function in your script, you must provide the parameters on the same command line as the function, like this:

```
func1 $value 10
```

The function can retrieve the parameter values using the parameter environment variables. Here's an example of using this method to pass values to a function:

```
$ cat test6
#!/bin/bash
# passing parameters to a function
function addem (
    if [ $$ -eq 0 ] || [ $$ -gt 2 ]
    then
        echo -1
    elif [ $$ -eq 1 ]
    then
        echo $[ $1 + $1 ]
    else
        echo $[ $1 + $2 ]
    fi
)

echo -n "Adding 10 and 15:"
value=`addem 15
echo $value
echo -n "Let's try adding just one number:"
value=`addem 10
echo $value
echo -n "Now trying adding no numbers:"
value=`addem
echo $value
```

370