This script uses the readPass function to read in a password from the user. The readPass function reads the password and stores it in the global variable PASS. The script then accesses the password using the variable PASS.

The readPass function is quite simple. It function starts by undefining PASS. Then it issues a prompt for the password and deactivates terminal echo using the stty -echo command. Terminal echo is deactivated because you don't want someone other than the user to inadvertently see the password. Next, you read the password and store its value in PASS by using the read command. Finally, you restore terminal echo using the stty echo command and echo a new line.

# Local Variables

Local variables are defined using typeset command:

`typeset var1=val1 ... varN=valN`

Here, var1 ... varN are variable names and val1 ... valN are values to assign to the variables. The values are optional as the following example illustrates:

```
```
typeset fruit1 fruit2=banana
```
```

This command declares two local variables, fruit1 and fruit2, and assigns the value banana to the variable fruit2.

The following script illustrates the behavior of local variables:

```
```bash
#!/bin/sh

pearFunc () {
    typeset pear=2;               # set $pear
    echo "In pearFunc(): pear is $pear"   # print out its value
}

pearFunc                        # call pearFunc
echo 'Outside of pearFunc(): pear is $pear'  # print out $pear
```
```

First, the script defines a function, pearFunc, which sets the value of a local variable $pear and outputs that value. Then the script executes pearFunc. Finally, the script prints the value of $pear outside of the function. The output is

In pearFunc(): pear is 2
Outside of pearFunc(): pear is

From the output, you can see that when the value of $pear is accessed within the pearFunc it has the value 2, but when the value of $pear is accessed outside the function, it has no value.