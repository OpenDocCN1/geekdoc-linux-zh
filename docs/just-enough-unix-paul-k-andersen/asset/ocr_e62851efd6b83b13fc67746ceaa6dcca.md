# CREATING SHELL SCRIPTS

24.4 A Daily Reminder System: tickle

```
```bash
#!/bin/sh
# A daily reminder service
set `date`
echo "Remember for today:"
case $1 in
  Mon) echo "Plan the week.";;
  Tue) echo "Take clothes to the cleaners.";;
  Wed) echo "Attend group meeting.";;
  Thu) echo "Make plans for the weekend."
        echo "Pick up clothes at the cleaners.";;
  Fri) echo "Answer e-mail.";;
  Sat) echo "You should not be here working."
        echo "Finish your work and log off.";;
  Sun) echo "Call Grandma and Grandpa.";;
esac
```
```

Listing 24-4B
The tickle script.

After studying the outline, create the script:

+   1. Use the text editor to create the script file. Open a file named *tickle* and enter the script shown in Listing 24-4B. Write and quit the file when finished.

+   2. Make the script executable. Use *chex* for this:

```
```
$ chex tickle (Return)
```
```

*tickle* is now executable:

-rwxr-xr-x 1 yourlogin 457 Date time *tickle*

+   3. Test the new script. Enter the *tickle* command:

```
```
$ tickle (Return)
```
```

This should print out the appropriate message for the day. However, we are not finished yet. A reminder service is not much good if you have to remember to type "*tickle*" to use it. It would be better to have the shell run the script automatically each time you log in.

+   4. If necessary, move the file *tickle* to your home directory. Recall that the variable *HOME* contains the pathname of your home directory:

```
```
$ mv tickle $HOME (Return)
```
```

+   5. Modify your login initialization file to execute *tickle*. Using the text editor, add the following line to your *,login* or *,profile*:

```
```
tickle
```
```

+   6. Execute your login initialization file. Use the source or "dot" command, as appropriate: