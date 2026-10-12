period and are not visible when using a normal ls command. These files are also known as *dot files*. They may also have an .rc extension. One example is the .bashrc file that starts programs at the bash prompt. However, hidden files are not limited to files with an .rc extension. Some other well-known startup files are .profile, .bash_profile, and .bash_login. These are the more standard startup files in each user's directories under Red Hat Linux.

# ## Defining Run Command Scripts

As an example of run command scripts, the sendmail file in the /etc/rc.d/init.d/ directory is actually a longer script that controls the manner in which sendmail operates. A quick look through the script shows that it has certain arguments for starting up the sendmail daemon. These flags and options can be modified to accommodate the user. Whenever you make changes to default settings, be sure to create a backup copy of the file just in case something goes wrong, such as a typing or misspelling error that leads to the script failing to execute correctly. Before you edit a file, you should copy it and give it another extension. I usually place a .dist extension at the end of my copied file. In this manner you will remember that the .dist extension stands for the *distribution* file that came pre-installed. For example, if you were about to make changes to the sendmail script in the /etc/rc.d/init.d/ directory, you would type the following:

```
cp /etc/rc.d/init.d/sendmail /etc/rc.d/init.d/sendmail.dist
```

This way you can always fix any mistakes or restore the distribution configuration without reinstalling the package. Backing up the file first can save many a headache.

After you copy the file using an alternative filename, you can begin editing it without fear. Looking through the sendmail script, it is clear that the script cleans up several different sendmail options before actually starting the daemon itself.

The daemon first reinitializes the aliases file and then rebuilds the virtual user table, or virtualuser table, database. The options associated with sendmail will be examined in greater detail later on. The script handles many of the mundane tasks automatically so that the user does not need to input all the commands by hand. This is fairly typical of most daemons spawned in the /etc/rc.d/init.d/ directory. See Chapter 18, “Sounding Off” on Linux,” for a more complete overview of the options associated with sendmail.