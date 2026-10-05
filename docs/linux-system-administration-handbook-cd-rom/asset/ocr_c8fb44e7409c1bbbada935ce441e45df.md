Here are some simple tcsh settings:

+   - autologout—After a certain amount of time (the option to autologout) of inactivity, log out the user. If a second number is included in the setting, the terminal will lock after the second number of minutes.
- history—Contains the number of commands stored in the history. Note that this is similar to HISTSIZE in bash.
- mail—contains the location of the mail spool directory (multiple ones) and prints "You have new mail."
- watch—Contains a list of user/terminal pairs that get monitored by tesh for a connection. You can replace the user or terminal with any to match all users or all terminals. If a match is made, the shell prompts you with a note saying who logged in and the terminal they logged in on. set=(any any) monitors all users on all terminals

# For Loops

For loops in csh are functionally the same as under sh. The loop iterates through all the items in the list until the list is complete. The command is slightly different (called foreach) and the syntax would be

```
foreach i (*)
  ls -la $i
end
```

# While Loops

While loops are also the same as under sh. As long as the starting condition is still true, the break command will allow you to break out of the loop completely, and the continue command will break out of the loop, but start processing at the while command again. If you use either of these commands, they have to be made within that loop.

```
while [-f /var/spool/mail/markk]
  echo "Mail exists in /var/spool/mail/markk" >> -markk/mail.file
  sleep 30
end
```