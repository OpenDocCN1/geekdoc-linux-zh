# EXAMPLE 12.2.3 (CONTINUED)

```
elif (( age >= 20 && age < 30 ))
then
    print "You got the world by the tail!!"
elif (( age >= 30 && age < 40 ))
then
    print "Thirty something..."
else
    print "Sorry I asked"
fi

(The Output)

$ tellme
How old are you? 200
Welcome to our planet!

$ tellme
How old are you? 13
Rebel without a cause

$ tellme
How old are you? 55
Sorry I asked
```

# EXPLANATION

+   1. The user is asked for input. The input is assigned to the variable age.
+   2. A numeric test is performed within the double parentheses. If age is less than 0 or greater than 120, the print command is executed and the program terminates with an exit status of 1. The interactive shell prompt will appear. Note that the dollar sign ($) is not required to perform variable substitution when using the (( )) operators.
+   3. A numeric test is performed within the double parentheses. If age is greater than 0 and less than 13, the let command returns exit status 0, true.
+   4. The else construct is the default. If none of the above statements are true, the else command will be executed.
+   5. The fi terminates the initial if statement.

# 12.5.14  The exit Command

The exit command is used to terminate the script and get back to the command line. You may want the script to exit if some condition does not test true. The argument to the exit command is an integer, ranging from 0 to 255. When the program exits, the exit number is stored in the shell's ? variable.