You can also get to the “Editing profile” dialog by selecting Edit | Current Profile, or Edit | Edit Profiles, and then selecting the profile of interest and clicking the Edit button. Or you can right-click in the command window and select Edit Current Profile from the context menu.

On the General tab, the profile icon is the image that displays in the panel when you have a command window running. You probably don’t want to change the font, since the default choice, monospace 12, looks okay and renders fixed-pitch strings nicely. Changing to a proportional font such as Arial can make it nearly impossible to distinguish between certain characters (the lowercase letter “l” and a number “1”, for example).

On the Title and Command tab, you can control what shows up in the title bar. Choices include the name of the profile in various combinations, with the default string of “username, hostname, and current directory.”

# The environment

An environment variable is a value set in the operating system and is available both interactively and to programs. For example, the shell program running in the command window is stored in an environment variable, and you can query it by using the “echo” command. On my system, if I type:

```
echo $SHELL
```

It returns:

```
/bin/bash
```

When I am developing software, I set up several environment variables to provide identification for my software. These variables indicate that the programs are running on a development machine as opposed to running on a user’s computer in production. When my software runs, it looks for those environment variables. If it finds them, certain “developer-only” functionality is available (such as debugging tools). If the software doesn’t find the variables, the software runs as if it’s on a user’s computer. By using environment variables, I can run the software both in development and production modes on the same machine.

Linux has environment variables much like those available in Windows. A number of environment variables are set automatically, and you can set up more yourself.

You can type “env” to see a listing of the system environment variables and type “set” to display all environment variables, shell functions, and aliases. You can also see any other command by using the “echo” command as mentioned earlier. Note that environment variable names are case-sensitive, so while

```
echo $PATH
```

returns

```
/usr/kerberos/bin:/usr/local/bin, etc.
```

the command

```
echo $path
```

returns nothing.