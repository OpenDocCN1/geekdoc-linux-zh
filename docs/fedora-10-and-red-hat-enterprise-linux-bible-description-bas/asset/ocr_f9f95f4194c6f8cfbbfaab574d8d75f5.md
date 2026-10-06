# Part I: Getting Started in Fedora RHEL

Type the following:

After that, the jobs run in the background. Its jobs entry appears as follows:

```
$ bg %5
[5] Running nroff -man man4*/ >tmp/man4 &
```

If you would like to run a job in the background, and have it continue to run after you exit the shell from which you ran it, you can run that command by preceding it with nohup command. For example, to update your locate base (where all store are on your system you can find easily with the locate command) so it will keep running after you exit the shell, type the following command:

```
# nohup updated &
```

# Configuring your shell

You can tune your shell to help you work more efficiently. Your prompt can provide pertinent information each time you press Enter. You can alias your keystrokes and permanently set environment variables to your needs. To make each change occur when you start a shell, you can add this information to your shell configuration files.

Several configuration files support how your shell behaves. Some of the files are executed for every user and every shell. Others are specific to the user who creates the configuration file. Here are the files of interest to those using the bash shell in Linux:

+   * /etc/profile— This file sets user environment information for every user. It is executed when you first log in. This file provides values for your path, as well as setting environment variables for such as the location of your mailbox and the size of your history files. Finally, /etc/profile gathers settings from configuration files in /etc/profile.d directory. Note that you can override all of these in start-up files.

+   * ~/.bashrc — By default, this file is executed for every user who runs the bash shell, each time a bash shell is opened. It sets the prompt and may add one or more aliases. Values in this file can be overridden by information in each user’s ~/.bashrc file.

+   * ~/.bash_profile — This file is used to specific to your own use of the shell. It is executed only once, when the user logs in. By default, it sets a few environment variables and executes the user’s .bashrc file. You can instead create a file named ~/.bash_login to serve the same purpose as ~/.bash_profile.

+   * ~/.bashrc — This file contains the information that is specific to your bash shells. It is read when you log in and each time you open a new bash shell. This is the best location to add environment variables and aliases so that your shell picks them up.