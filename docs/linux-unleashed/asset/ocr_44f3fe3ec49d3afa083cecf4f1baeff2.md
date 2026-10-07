These commands are most often used when a user wants to run a command in the back-ground but accidentally starts it in the foreground. When a command is started in the foreground, it locks the shell from any further user interaction until the command com-pletes execution. This is usually not a problem because most commands take only a few seconds to execute. If the command you are running takes a long time, though, start the command in the background so that you can continue to use bash to enter other com-mands in the foreground.

For example, if you start the command find / -name "test" > find.out (which scans the entire file system for files named test and stores the results in a file called find.out) in the foreground, your shell may be tied up for many seconds or even min-utes, depending on the size of the file system and the number of users on the system. If you issue this command and want to continue executing in the background so you can use the system again, enter the following:

```
control-z
bg
```

This first suspends the find command, then restarts it in the background. The find com-mand continues to execute, and you have bash back again.

# ## Customizing bash

Many ways of customizing bash have already been described in this chapter. Until now, the changes that you made affected only the current bash session. As soon as you quit, all of the customizations will be lost. You can, however, make the customizations more permanent by storing them in a bash initialization file.

You can put any commands that you want to be executed each time bash is started into this initialization file. Commands that are typically found in this file are alias com-mands and variable initializations.

The bash initialization file is named either .profile or .bash_profile, depending on the version of Linux you are using. For simplicity's sake, we'll assume .profile is used, although you should substitute the name your Linux system uses. Each user who uses bash has a .profile file in his home directory. This file is read by bash each time it starts, and all of the commands contained within it are executed.

Many Linux systems use a default profile file (note the lack of a period before the file-name). This file is located in the /etc directory and is read when you start bash. If you want to add your own customizations to bash, you must copy this file into your home directory (if it is not already there) and call it .profile.