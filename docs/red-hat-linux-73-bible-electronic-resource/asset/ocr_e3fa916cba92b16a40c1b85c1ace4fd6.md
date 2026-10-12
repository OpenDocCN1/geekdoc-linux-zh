The problem with setting environment variables in this way is that as soon as you exit the shell in which you set the variable, the setting is lost. To set variables more permanently, you should add variable settings to your bash configuration files, which is described later in the section on adding environment variables.

If you want to have other text right up against the output from an environment variable, you can surround the variable in braces. This protects the variable name from being misunderstood. For example, if you wanted to add a command name to the `AB` variable shown earlier, you could do the following:

```
```
$ echo $(AB)/adventure
/usr/dog/contagious/ringbearer/grind/adventure
```
```

Remember that you need to export the variable for it to be picked up by other commands. You need to add the export line to a shell configuration file for it to take effect the next time you log in. The `export` command is fairly flexible. Instead of running the `export` command after you set the variable, you could do it all in one step, as follows:

```
```
$ export XYZ=/home/xyz/bin
```
```

You can override the value of any environment variable at any time. This can be temporary by typing the new value in the shell. Or you can add the changed variable command line to your `$HOME/.bashrc` file. One useful variable to update is the `PATH` variable. Here is an example:

```
```
$ export PATH=$PATH:/home/xyz/bin
```
```

In this example, I temporarily added the `/home/xyz/bin` directory to the `PATH`. This is useful if, during a shell session, you find yourself wanting to run a bunch of commands from a directory that is not normally in your `PATH`. This temporary addition saves you from typing the full or relative path each time you want to run a command.

If you decide that you no longer want a variable to be set, you can use the `unset` command to erase its value. For example, you could type `unset XYZ`, which would cause `XYZ` to have no value set. (Remember to remove the `export` from the `$HOME/.bashrc` file — if you added it there — or it will return the next time you open a new shell.)

# ## Managing background and foreground processes

If you are using Linux over a network or from a *dumb terminal* (a monitor that allows only text input with no GUI support), your shell may be all that you have. You may be used to a windowing environment where you have a lot of programs active at the same time so that you can switch among them as needed. This shell thing can seem pretty limited.

Though the `bash` shell doesn’t offer you a GUI for running many programs, it does offer a way to move active programs between the background and foreground. In this way, you can have a lot of stuff running, while selectively being able to choose the one you want to deal with at the moment.