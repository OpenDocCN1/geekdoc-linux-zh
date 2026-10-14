After setting up a printer, you can print files from the command line using the lpr command.

# COMMAND SUMMARY

| Command | Description | Example |
|---|---|---|
| alias | Command within a shell that assigns a string of characters to a substitute string of characters | alias ll="ls -la" |
| echo | Prints text to the screen | echo "Hello" |
| env | Starts a program with an environment variable setting that is not part of your current environment | env DB_DIR=/data dbprogram |
| export | Makes a newly created environment variable available to other programs running in the same environment | export PS1="$ " |
| history | Displays all of the stored commands in the history list | history |
| lpoptions | Sets one or more options for the lpr command so that they can more easily be used in the future | lpoptions -P hplj -o media=legal -o job-sheets=confidential |
| lpr | Prints a file or piped input (sends data to a print queue, from which it is sent to a printer) | lpr .bashrc |
| mail | Command-line utility used to send or read e-mail messages | mail -s "My bashrc file" nwell@comcast.net < ~/.bashrc |
| set | Displays a list of all environment variables defined in the current environment | set |
| tee | Sends output to both a file and the screen | sort data_file | tee sorted_data |
| vi | Starts the vi command text editor; Tables 3-3 to 3-6 show vi commands | vi /etc/webalizer.conf.sample |
| wc | Displays the number of characters, words, and lines in a text file | wc /usr/share/dict/linux.words |

# Key Terms

.bashrc — A configuration script that is executed each time the user starts a bash shell.

.profile — A configuration script that can be located in each user's home directory. A script that is executed each time any user on the system starts a bash shell. This script is not included by default on all Linux distributions, but can be created if needed.

/etc/profile — A script containing configuration information that applies to every user on the Linux system.