```
    then
    echo "You won"
    else
    echo "You lost!"
    fi
```

This is a simple example showing the OR operator working in a Linux shell script. The user will only be declared a winner when the number 15 or 45 is input.

We use the || sign to denote the OR operator.

# ### How to Use Elif

The elif statemenet means "else-if" and is used to implement some chain logic. Have a look at this example to see how it works:

```
#!/bin/bash


echo -n "Enter a number: "
read num


if [[ $num -gt 10 ]]
then
    echo "Number is greater than 10."
elif [[ $num -eq 10 ]]
    then
    echo "Number is equal to 10."
else
    echo "Number is less than 10."
fi
```

This is a self-explanatory example, so I won't go into too much detail. You can play around and change the variable names or their values to see how they function.

# ### How to Use the Switch Construct

This is another very powerful construct in Linux scripts, and you can use it when you need to use nested conditions, but you don't want to write complicated of-else-elif chains. Here is an example of how it works.

```
#!/bin/bash


echo -n "Enter a number: "
read num

case $num in
    100)
        echo "Hundred!" ;;
    200)
        echo "Double Hundred!" ;;
```