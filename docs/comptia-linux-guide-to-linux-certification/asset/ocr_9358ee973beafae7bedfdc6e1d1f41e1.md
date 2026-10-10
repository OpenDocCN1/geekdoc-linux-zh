+   3. At the command prompt, type `cat /etc/nsswitch.conf | grep nisplus` and press Enter. How many lines are displayed? Why did you not need to specify a filename with the `grep` command?
+   4. At the command prompt, type `cat /etc/nsswitch.conf | grep nisplus | tr n N` and press Enter. Explain the output on the terminal screen.
+   5. At the command prompt, type `cat /etc/nsswitch.conf | grep nisplus | tr n N | sort -r` and press Enter. Explain the output on the terminal screen.
+   6. At the command prompt, type `cat /etc/nsswitch.conf | grep nisplus | tr n N | sort -r | tee file` and press Enter. Explain the output on the terminal screen. Next, type `cat file` at the command prompt and press Enter. What are the contents? Why? What does the `tee` command do in the pipe above?
+   7. At the command prompt, type `cat /etc/nsswitch.conf | grep nisplus | tr n N | sort -r | tee file` and press Enter. Explain the output on the terminal screen. Next, type `cat file` at the command prompt and press Enter. What are the contents and why?
+   8. At the command prompt, type `cat /etc/nsswitch.conf | grep nisplus | sed /#/d | sed /public/;s//NISP/;NISPPLUS` and press Enter. Explain the output on the terminal screen. Can this output be obtained with the `grep` and `tr` commands instead of `sed` ?
+   9. At the command prompt, type `cat /etc/hosts`. Next, type `cat /etc/hosts | awk '{print $1, $3}'` and press Enter. Explain the output on the terminal screen.
+   10. Type `exit` and press Enter to log out of your shell.

# Project 7-3

In this hands-on project, you create and use an alias, as well as view and change existing shell variables. In addition to this, you export user-defined variables and load variables automatically upon shell startup.

+   1. Switch to a command-line terminal (tty2) by pressing Ctrl+Alt+F2 and log in to the terminal using the user name of root and the password of LNXrocks!.
+   2. At the command prompt, type `set | less` and press Enter to view the BASH shell environment variables currently loaded into memory. Scroll through this list using the cursor keys on the keyboard. When finished, press q to quit the less utility.
+   3. At the command prompt, type `env | less` and press Enter to view the exported BASH shell environment variables currently loaded into memory. Scroll through this list using the cursor keys on the keyboard. Is this list larger or smaller than the list generated in Step 2? Why? When finished, press q to quit the less utility.
+   4. At the command prompt, type `PS1="Hello There:"` and press Enter. What happened and why? Next, type `echo $PS1` at the command prompt and press Enter to verify the new value of the PS1 variable.
+   5. At the command prompt, type `exit` and press Enter to log out of the shell. Next, log in to the terminal using the user name of root and the password of LNXrocks!. What prompt did you receive and why? How could you ensure that next time the "Hello There: " prompt occurs at every login?