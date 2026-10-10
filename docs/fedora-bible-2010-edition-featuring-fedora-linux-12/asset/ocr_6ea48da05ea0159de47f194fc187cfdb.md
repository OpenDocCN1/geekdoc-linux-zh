You can use several special characters (indicated by adding a backslash to a variety of letters) to include different information in your prompt. These can include your terminal number, the date, and the time, as well as other pieces of information. Here are some examples:

+   * `\!` — Shows the current command history number. This includes all previous commands stored for your user name.
+   * `\#` — Shows the command number of the current command. This includes only the commands for the active shell.
+   * `\$` — Shows the user prompt ($) or root prompt (#), depending on which user you are. Note that `\$` is specially set up at login. After login, using `\$` will result in a prompt with a dollar sign. The special support for # occurs only in the shell start-up files.
+   * `\w` — Shows only the current working directory base name. For example, if the current working directory was `/var/spool/mail`, this value would simply appear as `mail`.
+   * `\[` — Precedes a sequence of nonprinting characters. This could be used to add a terminal control sequence into the prompt for such things as changing colors, adding blink effects, or making characters bold. (Your terminal determines the exact sequences available.)
+   * `\]` — Follows a sequence of nonprinting characters.
+   * `\\` — Shows a backslash.
+   * `\d` — Displays the day, month, and number of the date. For example: Sat Jan 23.
+   * `\h` — Shows the hostname of the computer running the shell.
+   * `\n` — Causes a newline to occur.
+   * `\nnn` — Shows the character that relates to the octal number replacing `nnn`.
+   * `\s` — Displays the current shell name. For the bash shell, the value would be `bash`.
+   * `\t` — Prints the current time in hours, minutes, and seconds (for example, 10:14:39).
+   * `\u` — Prints your current user name.
+   * `\w` — Displays the full path to the current working directory.

> TIP: If you are setting your prompt temporarily by typing at the shell, you should put the value of PS1 in quotes. For example, you could type `export PS1="[\t \w]\$ ">` to see a prompt that looks like this: `[20:26:32 /var/spool]$`.

To make a change to your prompt permanent, add the value of PS1 to your .bashrc file in your home directory (assuming that you are using the bash shell). There may already be a PS1 value in that file that you can modify. Refer to the Bash Prompt HOWTO (http://www.tldp.org/HOWTO/Bash-Prompt-HOWTO) for information on changing colors, commands, and other features for your bash shell prompt.