```
*\)
    echo "Neither 100 nor 200";;
    esac
```

The conditions for a switch are places between the case and esac keywords.
The condition is then placed before the ) symbol.

# ## Concatenation

Concatenation is a function of the wider term that is known as string
processing. String processing is playing with strings such that you can get the
desired output. Concatenation is a string processing function that appends
two or more strings together. Let’s have a look at an example.

```
#!/bin/bash
string1="Ubuntu"
string2="Linux"
string=$string1$string2
echo "$string is a great operating system for Linux beginners."
```

The output of the above script will be “UbuntuLinux is a great operating
system for Linux beginners ”

# ## Adding Two Numbers

Linux scripts are very easy to perform arithmetic operations. The script given
below takes two numbers as inputs from the user, adds them, and prints the
sum.

```
#!/bin/bash
echo -n "Enter first number:"
read x
echo -n "Enter second number:"
```