
## Project 7-2

In this hands-on project, you redirect Standard Output and Standard Input using pipe metacharacters.

- Switch to a command-line terminal (tty2) by pressing `Ctrl+Alt+F2` and log in to the terminal using the user name of `root` and the password of LNXrocks!.
- At the command prompt, type `cat /etc/nsswitch.conf` and press `Enter` to view the `/etc/nsswitch.conf` file. Next, type `cat /etc/nsswitch.conf | less` at the command prompt and press `Enter` to perform the same task page-by-page. Explain what the `|` metacharacter does in the previous command. How is this different from the `less /etc/nsswitch.conf` command?
- At the command prompt, type `cat /etc/nsswitch.conf | grep nisplus` and press `Enter`. How many lines are displayed? Why did you not need to specify a filename with the `grep` command?
- At the command prompt, type `cat /etc/nsswitch.conf | grep nisplus | tr n N` and press `Enter`. Explain the output on the terminal screen.
- At the command prompt, type `cat /etc/nsswitch.conf | grep nisplus | tr n N | sort -r` and press `Enter`. Explain the output on the terminal screen.
- At the command prompt, type `cat /etc/nsswitch.conf | grep nisplus | tr n N | sort -r | tee file` and press `Enter`. Explain the output on the terminal screen. Next, type `cat file` at the command prompt and press `Enter`. What are the contents? Why? What does the `tee` command do in the pipe above?
- At the command prompt, type `cat /etc/nsswitch.conf | grep nisplus | tr n N | sort -r | tee file` and press `Enter`. Explain the output on the terminal screen. Next, type `cat file` at the command prompt and press `Enter`. What are the contents and why?
- At the command prompt, type `cat /etc/nsswitch.conf | grep nisplus | sed /#/d | sed /public/;s//NISP/;NISPPLUS` and press `Enter`. Explain the output on the terminal screen. Can this output be obtained with the `grep` and `tr` commands instead of `sed`?
- At the command prompt, type `cat /etc/hosts`. Next, type `cat /etc/hosts | awk '{print $1, $3}'` and press `Enter`. Explain the output on the terminal screen.
- Type `exit` and press `Enter` to log out of your shell.

## Project 7-3

In this hands-on project, you create and use an alias, as well as view and change existing shell variables. In addition to this, you export user-defined variables and load variables automatically upon shell startup.

- Switch to a command-line terminal (tty2) by pressing `Ctrl+Alt+F2` and log in to the terminal using the user name of `root` and the password of LNXrocks!.
- At the command prompt, type `set | less` and press `Enter` to view the BASH shell environment variables currently loaded into memory. Scroll through this list using the cursor keys on the keyboard. When finished, press `q` to quit the `less` utility.
- At the command prompt, type `env | less` and press `Enter` to view the exported BASH shell environment variables currently loaded into memory. Scroll through this list using the cursor keys on the keyboard. Is this list larger or smaller than the list generated in Step 2? Why? When finished, press `q` to quit the `less` utility.
- At the command prompt, type `PS1="Hello There:"` and press `Enter`. What happened and why? Next, type `echo $PS1` at the command prompt and press `Enter` to verify the new value of the PS1 variable.
- At the command prompt, type `exit` and press `Enter` to log out of the shell. Next, log in to the terminal using the user name of `root` and the password of LNXrocks!. What prompt did you receive and why? How could you ensure that next time the "Hello There:" prompt occurs at every login?
- At the command prompt, type `vi .bash_profile` and press `Enter`. At the bottom of the file, add the following lines. When finished, save and quit the vi editor.

```bash
echo -e "\nWould you like a hello prompt? (y/n) --> "
read ANSWER
if [ $ANSWER = "y" ]
then
PS1="Hello There: "
fi
```

Explain what the preceding lines will perform after each login.

- At the command prompt, type `exit` and press `Enter` to log out of the shell. Next, log in to the terminal using the user name of `root` and the password of `LNXRocks!`. When prompted for a hello prompt, type `y` and press `Enter`. What prompt did you receive and why?
- At the command prompt, type `exit` and press `Enter` to log out of the shell. Next, log in to the terminal using the user name of `root` and the password of `LNXRocks!`. When prompted for a hello prompt, type `n` and press `Enter` to receive the default prompt.
- At the command prompt, type `MYVAR="My sample variable"` and press `Enter` to create a variable called MYVAR. Verify its creation by typing `echo $MYVAR` at the command prompt, and press `Enter`.
- At the command prompt, type `set | grep MYVAR` and press `Enter`. Is the MYVAR variable listed? Why?
- At the command prompt, type `env | grep MYVAR` and press `Enter`. Is the MYVAR variable listed? Why?
- At the command prompt, type `export MYVAR` and press `Enter`. Next, type `env | grep MYVAR` at the command prompt and press `Enter`. Is the MYVAR variable listed now? Why?
- At the command prompt, type `exit` and press `Enter` to log out of the shell. Next, log in to the terminal using the user name of `root` and the password of `LNXRocks!`.
- At the command prompt, type `echo $MYVAR` and press `Enter` to view the contents of the MYVAR variable. What is listed and why?
- At the command prompt, type `vi .bash_profile` and press `Enter`. At the bottom of the file, add the following line. When finished, save and quit the vi editor.

```bash
export MYVAR="My sample variable"
```

- At the command prompt, type `exit` and press `Enter` to log out of the shell. Next, log in to the terminal using the user name of `root` and the password of `LNXRocks!`.
- At the command prompt, type `echo $MYVAR` and press `Enter` to list the contents of the MYVAR variable. What is listed and why?
- At the command prompt, type `alias` and press `Enter`. What aliases are present in your shell?
- At the command prompt, type `alias asample="cd /etc ; cat hosts ; cd - ; ls -F"` and press `Enter`. What does this command do?
- At the command prompt, type `asample` and press `Enter`. What happened and why? What environment file could you add this alias to such that it is executed each time a new BASH shell is created?
- Type `exit` and press `Enter` to log out of your shell.
