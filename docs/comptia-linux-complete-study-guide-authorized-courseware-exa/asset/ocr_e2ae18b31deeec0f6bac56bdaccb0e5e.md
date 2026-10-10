![](bbox=[0.15, 0.1, 0.25, 0.2])

> Be careful when changing your bash configuration, and particularly the global bash configuration files. Save a backup of the original file before making changes, and test your changes immediately by logging in using another virtual terminal. If you spot a problem, revert to your saved copy until you can learn the cause and create a working file.

# ## Using Environment Variables

Environment variables are like variables in programming languages—they hold data to be referred to by the variable name. Environment variables differ in that they're part of the environment of a program, and other programs, such as the shell, can modify this environment. Programs can rely on environment variables to set information that can apply to many different programs. For instance, suppose a computer hosts several different Usenet news readers. These programs all need to know what Usenet news server to use; if they all agree to use an environment variable, such as $NTPSERVER, to hold this information, you can set this environment variable once as part of your shell startup script and then forget it. You needn't set this feature individually for all the news readers installed on the system.

Chapter 9 describes environment variables and their manipulation in more detail. For the moment, you should know that you can set them in bash by using an assignment (=) operator followed by the `export` command:

```
$ NTPSERVER=news.abigisp.com
$ export NTPSERVER
```

You can combine these two commands into a single form:

```
$ export NTPSERVER=news.abigisp.com
```

Either method sets the $NTPSERVER environment variable to news.abigisp.com. (When setting an environment variable, you omit the dollar sign, but subsequent references include a dollar sign to identify the environment variable as such.) Hereafter, programs that need this information can refer to the environment variable. In fact, you can do so from the shell yourself, using the `echo` command:

```
$ echo $NTPSERVER
news.abigisp.com
```

You can also view the entire environment by typing `env`. The result is likely to be several dozen lines of environment variables and their values. Chapter 9 describes what many of these variables are in more detail.

To delete an environment variable, use the `unset` command, which takes the name of an environment variable (without the leading $ symbol) as an option. For instance, `unset NTPSERVER` removes the $NTPSERVER environment variable.