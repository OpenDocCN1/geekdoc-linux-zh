Now armed with this information, you could move or copy the file in question to one of the directories listed by the echo $PATH command, as in Listing 0-1, and then the command will run. We use which throughout the book to determine the full path to commands. It’s a useful tool for debugging a broken or weird PATH.

# # Configuring Your Login Script

Throughout the book, we will be writing scripts that we will then use in other scripts, so being able to easily call your new scripts is important. You can configure your PATH variable so that your custom scripts are automatically shell, just like any other command, when you start a new command shell. When you open a command shell, it does is read a login script in your home directory (/Users/<username> or /home/<username> in OS X or Linux, respectively) and execute any custom commands it finds there. The login script will be .login, .profile, .bash_profile, or .bash_profile, depending on your shell. The login script, add a line like the following to each file:

```
echo this is .profile
```

Tweak the last word to match the name of the file and then log in. The line should be printed at the top of the terminal window, reporting which script was run at login. If you open a terminal and see this is .profile, you know the .profile file is being loaded for your shell environment; if you see this is .bashrc, you know it’s the .bashrc file; and so on. And now you know! This behavior can change, though, depending on your shell.

You can alter the login script so it configures your PATH variable with other directories. You can also set up all kinds of bash settings, from changing how the bash prompt looks to setting a custom PATH to any number of other customizations. For instance, let’s use the cat command to take a look at a customized .bashrc login script. The cat command takes a filename as an argument and prints the contents of the file to the console screen, as shown in Listing 0-3.

```
$ cat ~/.bashrc
export PATH="$PATH:$HOME/.rvm/bin" # Add RVM to PATH for scripting.
```

Listing 0-3: This code displays the contents of the .bashrc file, showing that a new value has been assigned to PATH that allows the local RVM (Ruby version manager) installation to manage any installed Ruby versions. Because the .bashrc file sets the customized PATH every time a new command shell is opened, the RVM installation will be available by default on this system.

You can implement a similar customization to make your shell scripts available by default. First, you’ll create a development folder in your home directory to save all your shell scripts in. Then you can add this directory to PATH in your login file to reference your new scripts more easily.