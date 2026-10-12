
directory. Here are two typical examples of bash prompts. The first example shows a regular user logged in to a machine called pluto. His current location is the /etc directory. The second example shows the root user logged in to a machine called goofy while in his home directory.

```
[kerry@pluto /etc]$   [root@goofy /root]#
```

Notice the character just outside the brackets. The dollar sign ($) is reserved for regular users. The pound sign (#) is assigned only to root or superuser. Setting these symbols at the shell prompt is fairly standard practice on all Linux machines.

The latest version of Red Hat provides even more functionality and is far more descriptive in defining where a user is located. The shell prompt still appears the same. However, when a user is logged in to an xterm (or one of the many terminal window emulators such as rxvt, aterm, or Eterm), the title bar above the terminal window displays not only the user's name and the machine he or she is logged in to, but also the full path name of the user's current working directory.

Customizing the shell prompt can prove entertaining as well as functional. You can specify exactly what variable you want visible and just how much information to provide. Besides specifying that the prompt display local information, you can also have the prompt print out messages such as who is logged in to the machine or have it print one of the many quotes found in the fortune program. To keep things fairly standard, bash provides the user with some arguments that he or she can be then incorporate into the user's profile. Normally, bash reads the user's own profile for customized settings. This file is one of the dot, or hidden, files. It is usually called .bash_profile, but on some machines that do not use bash as their default, its name is .profile. If there is no .bash_profile or .profile file located in the user's home directory, then the shell looks to /etc/profile for the global settings and uses the standards there. Users logging in to other shells, such as sh, can find a .sh_profile hidden file. The line in this file that determines the appearance and functionality of the prompt begins with $1. There is also sometimes a $2 line that provides additional information that is needed to serve a request. For example, if you do not complete a shell command or split a command across lines, such as hitting the Enter button before a closing quote, you will be given a secondary prompt. PS2 defines the appearance of that prompt. Table 4.3 describes the available settings in the prompt string; you can find more detail in the man page for bash.

### TERMINAL SHELLS

Table 4.3 A Brief Summary of Available Settings that Can Be Used to Define the bash Prompt

| Variable | Definition |
| :--- | :--- |
| \t | The current time in HH:MM:SS format. |
| \d | The date in “weekday month date” format (eg, “Tue May 26”). |
| \n | Newline. |
| \s | The name of the shell, (the portion following the final slash). |
| \w | The current working directory. |
| \W | The basename of the current working directory. |
| \u | The username of the user currently logged in. |
| \h | The hostname. |
| \# | The command number of this command. |
| \! | The history number of this command. |
| \$ | The user type. If the effective UID is 0, a pound sign (#) will appear after the prompt; otherwise a dollar sign ($) is used. The former indicates a root user, the latter a normal user without root powers. |
| \nnn | The character corresponding to the octal number nnn. |
| \\ | A backslash. |
| \[ | The beginning of a sequence of nonprinting characters, which could be used to embed a terminal control sequence into the prompt. |
| \] | The end of a sequence of nonprinting characters. |

The following example, which draws from many of the commands described in Table 4.2, is one of the more standard methods that Linux uses to create a customized prompt string:

```
PS1='[\u@\h \W] \$ '
```

The preceding example creates the following prompt:

```
[kerry@pluto /etc]$
```

Setting the variable foo=bar makes foo available to users. It does not need to be exported. Exporting the variable PS1 also makes it available to the children of the shell. It is then a variable or component of that shell and as such exercises certain control over shell features, such as the default editor, path, or, in this case, prompt.

### NOTE

Putting these variables together in different combinations is a good method of becoming familiar with their use. By including the path in your prompt, you can become more familiar with the directory structures and where files are located.

Other users might want to create a more unique prompt that still provides information and functionality. Listing 4.4 shows a customized setup that I used to enable multiple users to log in under the shell of their choice. After setting up a user, this file, called .profile, was created in every user's directory by default. Here each user could define what prompt to use depending upon the environment settings. If a user has a certain shell defined in his or her dot file, then the prompt would be modified to provide additional information while allowing the user to retain the shell of his or her choice.

### Listing 4.4 A Sample Profile that Caters to Each User's Choice of Shells

```
# This is the default standard profile provided to users.
# They are expected to modify this file to meet their own needs.
if [ "$SHELL" = "/bin/pdksh" -o "$SHELL" = "/bin/ksh" ]; then
    elif [ "$SHELL" = "/bin/sh" ]; then
PS1='`&m:%-%# '
    elif [ "$SHELL" = "/bin/ash" ]; then
PS1='$ '
else
PS1='\h:\w\$ '
fi
PS2='> '
export PS1 PS2

#
# End of file
```

Note the presence of both a PS1 and a PS2 option in Listing 4.4's configuration. Though not often used, these options can be set to provide additional settings. Again, the PS2 setting is the line continuation option and displays a simple `>' sign when the command extends beyond the range of the command. The default

bash prompt would now appear as follows if a normal user were logged in to the Linux box called pluto and had a current working directory of /usr/local:

```
pluto:/usr/local$
```

This method is more verbose and shows the absolute path. However, when the working directory is several directories deep, the prompt can take up much of the line. Choosing your customized prompt requires some experimentation to determine what works best for your own needs.

### Additional Bash-ful Traits

The bash shell has many additional features aside from the customizable prompt that make it currently the most popular Linux shell. Again, because most everything under Linux is classified as open-source, anyone can add new and improved functions to the program. If something does not operate correctly, the source is available for all to see and thus correct. Such is the power of making code accessible for all.

### Tracking the Shell’s Command History

One of bash’s most popular features is its ability to keep track of commands entered at the command line. Essentially, every command entered at the prompt is stored in a file within the user’s home directory. This gives bash a distinct advantage over other shells. Knowing the commands last typed allows you not only to track the most recent entries, but also to redo commonly used commands.

If, during one bash session, you enter several commands and then want to reissue the same commands later, you do not have to enter in the same string of words or characters. You can selectively reuse your earlier commands by pressing the up-arrow key until you find the previously entered command. Each time that you press the up-arrow key, the prompt displays the commands that were entered just before the currently displayed ones.

> TIP  
> Using default emacs keys under the bash shell. Ctrl+R performs a reverse search through old commands. Start typing any part of the command and it will complete the command, locating the most recent command that matches your inquiry.
