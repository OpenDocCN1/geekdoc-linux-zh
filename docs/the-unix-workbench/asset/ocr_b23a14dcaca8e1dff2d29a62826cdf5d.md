# ## New York

Occasionally you might want to run a command like you would on the command line and store the result of that command in a variable. We can do this by wrapping the command in a dollar sign and parentheses $( ) around a command. This syntax is called command substitution. The command is executed and then gets replaced by the string that resulted from running the command. For example if we wanted to store the number of lines in math.sh:

```
math_lines=$(cat math.sh | wc -l)
echo $math_lines
```

# ## 7

Variable names with a dollar sign can also be used inside other strings in order to insert the value of the variable into the string:

```
echo "I went to school in $the_empire_state."
```

# ## I went to school in New York.

When writing a Bash script, the script gives you a few variables for free. Let’s create a new file called vars.sh with the following code: