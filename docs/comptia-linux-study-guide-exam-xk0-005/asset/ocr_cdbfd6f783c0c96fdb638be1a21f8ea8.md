The *case* statement compares the variable specified against the different patterns. If the variable matches the pattern, the shell executes the commands specified for the pattern. You can list more than one pattern on a line, using the bar operator to separate each pattern. The asterisk symbol is the catchall for values that don't match any of the listed patterns. Listing 25.12 shows an example of using the *case* statement.

# **Listing 25.12:** The *case* statement

```
```bash
$ cat test6.sh
#!/bin/bash
# using the case statement

case $USER in
    rich | barbaro)
        echo "Welcome, $USER"
        echo "Please enjoy your visit";;
    testing)
        echo "Special testing account";;
    jessica)
        echo "Don't forget to log off when you're done";;
    *)
        echo "Sorry, you're not allowed here";;
    esac
$ chmod u+x test6.sh
$ ./test6.sh
Welcome,  rich
Please enjoy your visit
$
```

The *case* statement provides a much cleaner way of specifying the various options for each possible variable value. In the example shown in Listing 25.12, it checks for specific user accounts to output specific messages. If the user running the script is not one of those user accounts, it displays yet another message.

# ## Loops

When you're writing scripts, you'll often find yourself in a situation where it would come in handy to repeat the same commands multiple times, such as applying a command against all the files in a directory. The Bash shell provides some basic looping commands to accommodate that.