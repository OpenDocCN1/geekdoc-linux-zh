```
count=1
echo "This line comes before the function definition"

function func1 {
    echo "This is an example of a function"
}

while [ $count -le 5 ]
do
    func1
    count=$[ $count + 1 ]
done
echo "This is the end of the loop"
func2
echo "Now this is the end of the script"

function func2 {
    echo "This is an example of a function"
}
$ 
$ ./test2 
This line comes before the function definition 
This is an example of a function 
This is an example of a function 
This is an example of a function 
This is an example of a function 
This is an example of a function 
This is the end of the loop 
./test2: func2: command not found 
Now this is the end of the script 
$
```

The first function, func1, was defined after a couple of statements in the script, which is perfectly fine. When the func1 function was used in the script, the shell knew where to find it.

However, the script attempted to use the func2 function before it was defined. Because the func2 function wasn't defined, when the script reached the place where we used it, it produced an error message.

You also need to be careful about your function names. Remember, each function name must be unique, or you'll have a problem. If you redefine a function, the new definition overrides the original function definition, without producing any error messages: