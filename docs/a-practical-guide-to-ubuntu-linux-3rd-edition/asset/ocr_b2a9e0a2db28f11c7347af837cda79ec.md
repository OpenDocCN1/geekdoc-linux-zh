The following locktty script is similar to the lock command on Berkeley UNIX and the Lock Screen menu selection in GNOME. The script prompts for a key (password) and uses an until control structure to lock the terminal. The until statement causes the system to ignore any characters typed at the keyboard until the user types the key followed by a RETURN on a line by itself, which unlocks the terminal. The locktty script can keep people from using your terminal while you are away from it for short periods of time. It saves you from having to log out if you are concerned about other users using your login.

```
```
$ cat locktty
#!/ /bin/bash

trap '' 1 2 3 18
stty -echo
echo -n "Key: "
read key_1
echo
echo -n "Again: "
read key_2
echo
key_3=
if [ "$key_1" = "$key_2" ]
then
	tput clear
	until [ "$key_3" = "$key_2" ]
	do
		read key_3
	done
else
	echo "locktty: keys do not match" 1>&2
fi
stty echo
```
```

# Forget your password for locktty?

> tip If you forget your key (password), you will need to log in from another (virtual) terminal and kill the process running locktty.

trap builtin The trap builtin (page 1009) at the beginning of the locktty script stops a user from being able to terminate the script by sending it a signal (for example, by pressing the interrupt key). Trapping signal 18 means that no one can use CONTROL-Z (job control, a stop from a tty) to defeat the lock. Table 27-5 on page 1009 provides a list of signals. The stty -echo command causes the terminal not to display characters typed at the keyboard, preventing the key the user enters from appearing on the screen. After turning off keyboard echo, the script prompts the user for a key, reads it into the user-created variable key_1, prompts the user to enter the same key again, and saves it in key_2. The statement key_3= creates a variable with a NULL value. If key_1 and key_2 match, locktty clears the screen (with the tput command)