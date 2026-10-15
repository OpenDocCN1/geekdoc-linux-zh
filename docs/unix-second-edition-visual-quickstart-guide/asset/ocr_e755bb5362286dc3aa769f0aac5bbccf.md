# Looking at Your bash Configuration Files

Your first step in modifying or adding bash environment variables in your configuration files is to look at the configuration files, which show you the variables that have been defined.

As Code Listing 8.10 shows, you do this using more or the editor of your choice.

Remember that configuration files run in a specific order:

+   - Systemwide configuration files (such as /etc/profile) run first upon log in.
+   - Configuration files specific to your Unix account (such as ~/.bash_profile or ~/.profile) run next if they're available.

# To look at your bash configuration files:

+   1. more ~/.bash* ~/.profile
+      +/etc/bash* /etc/profile

At the shell prompt, type more followed by each of the possible system configuration filenames to view your configuration files. If you don't have all of the files mentioned here, don't worry. Just make note of the ones you do have. Code Listing 8.10 shows an example of what you might see. Notice that some of the lines will reference other files, like the ENV=$HOME/.bashrc line that references the .bashrc file, containing other configuration settings.

continued on next page

```
[ejr@hobbes ejr]$ more ~/.bash* ~/.profile /etc/bash* /etc/profile
...
/home/ejr/.bash_profile
...
# .bash_profile
# Get the aliases and functions
```

Code Listing 8.10 Your configuration files set up your environment variables and other features of your Unix experience.