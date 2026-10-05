# Chapter 11 • Creating Scripts

(described shortly), variables become even more powerful, because then your script can perform one action when one is met and another in some other case. For instance, a script that installs software can check free disk space and abort the installation if insufficient disk space is available.

In addition assigning variables with the assignment operator (=), you can read variables from standard input by using read, as in response to input for subsequent access as $variable. This method of variable assignment is useful for scripts that must interact with users. For instance, instead of reading the username from the command line. Listing 11.2 shows the result. To use this script, you type its name without typing a username on the command line. The script will then prompt for a username and, after you enter one, the script will attempt to create an account with that name.

Certification Objective

LISTING 11.4: Modified version of Listing 11.2 that employs user interaction

```
#!/bin/bash
echo -n "Enter a username:"
read name
useradd -m $name
mdir -p /shared/$name
chown $name:users /shared/$name
chmod 775 /shared/$name
ln -s /shared/$name /home/$name/shared
chown $name:users /home/$name/shared
```

One special type of variable is an environment variable, which is assigned and accessed just like a shell variable. The difference is that the script or command sets an environment variable uses Bash's export command to make the value of the variable accessible to programs launched from the shell or shell script that made the assignment. In other words, you can set an environment variable in one script and use it in another script the first script launches. Environment variables are often set in shell startup scripts, but the scripts you use access for. If your script calls X programs, it might check for the presence of a valid $DISPLAY environment variable and abort if it finds that this variable isn't set. By convention, environment variable names are all uppercase, whereas nonenvironment shell script variables are all lowercase or mixed case.

One special variable deserves mention: $?. This holds the exit status (or return value) of the most recently executed command. Most programs return a value of 0 when they terminate normally and return another value to specify errors. You can display this value with echo or use it in a conditional expression (described next) to have your script perform special handling.

Consult a program's man page to learn the meanings of its return values.

![](bbox=[0.07, 0.856, 0.215, 0.888])