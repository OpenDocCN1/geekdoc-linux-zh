# Looking at Your csh Configuration Files

As Code Listing 8.18 (on the next page) shows, you can use more or the editor of your choice to peek at your csh configuration files. As with other shells, the csh configuration files run in a specific order:

+   - Systemwide configuration files (such as /etc/csh.cshrc) are read first upon log in.
+   - The main configuration files specific to your Unix account (~/ .cshrc) are read next if they’re available.
+   - The ~/.login configuration file is read last.

# To look at your csh configuration files:

+   - more .cshrc .login
+     Type more followed by .cshrc and .login which are the only possible names for csh configuration files. You’ll see something similar to Code Listing 8.18. For our system, we have
+     ▲ ~/.cshrc (automatically called by the system)
+     ▲ ~/.login (automatically called by the system) if the shell is a log-in shell

Tip

+   - The .cshrc file is executed when you start a new csh shell of any kind. The .login file is executed when you start a new log-in shell (by logging in or with su - yourid).

# Fill in Your csh System Configuration Files