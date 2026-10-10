continues (the user does not have to press the Enter key), assigning the entered data to the variable:

```
```
$ cat continueornot.sh
#!/bin/bash
# Using the read command for one character
#
read -n 1 -p "Do you want to continue [Y/N]? " answer
case $answer in
Y | y) echo
     echo "Okay. Continue on...";;
N | n) echo
     echo "Okay. Goodbye"
     exit;;
esac
echo "This is the end of the script."
exit
```

```plaintext
$ ./continueornot.sh
Do you want to continue [Y/N]? Y
Okay. Continue on...
This is the end of the script.
```

```plaintext
$ ./continueornot.sh
Do you want to continue [Y/N]? n
Okay. Goodbye
```

```

This example uses the `-n` option with the value of 1, instructing the `read` command to accept only a single character before continuing. As soon as you press the single character to answer, the `read` command accepts the input and passes it to the variable. You don’t need to press the Enter key.

# Reading with no display

Sometimes you need input from the script user, but you don’t want that input to display on the monitor. The classic example is when entering passwords, but there are plenty of other types of data that you need to hide.

The `-s` option prevents the data entered in the `read` command from being displayed on the monitor; actually, the data is displayed, but the `read` command sets the text color to the same as the background color. Here’s an example of using the `-s` option in a script:

```
```
$ cat askpassword.sh
#!/bin/bash
# Hiding input data
#
read -s -p "Enter your password: " pass
echo
echo "Your password is $pass"
exit
```

```