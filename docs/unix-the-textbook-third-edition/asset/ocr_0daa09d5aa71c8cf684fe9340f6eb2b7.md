```
while ( "$secretcode" != "$yourguess" )
    clear
    echo -n "Enter the code word: "
    set yourguess = `head -1`
end

# Set terminal to echo mode
clear
echo "Back again!"
stty echo
exit 0
%
```

You can use this script to lock your terminal before you leave it to pick up a printout or get a can of soda; hence, the name canleave (can leave). Using it saves you the time otherwise required for the logout and login procedures.

# 15.6 DEBUGGING SHELL PROGRAMS

You can debug your C shell scripts by using the -x (echo) option of the csh command. This option displays each line of the script after variable substitution but before execution. You can combine the -x option with the -v (verbose) option to display each command line of the script, as it appears in the script file before its execution. You can also invoke the csh command from the command line to run the script, or you can make it part of the script, as in #!/bin/csh -xv.

In the following session, we show how a shell script can be debugged. The script in the debug_demo file prompts you to enter a digit. If you enter a value between 1 and 9, it displays a message informing you that what you entered was good and quits. If you enter any other value, it informs you accordingly and exits. When we execute the script and enter 4, a valid input, it displays the message var1cat: Undefined variable. Similarly, when we run the script and enter 10, an invalid input, we get the same error message.

```
% cat debug_demo
#!/bin/csh
echo -n "Enter a digit: "
set var1 = `head -1`
if (($var1 >= 1) && ($var1 <= 9)) then
    echo "Good input is $var1!!"
else
    echo "Bad input is $var1!!"
endif
exit 0
% ./debug_demo
Enter a digit: 4
```