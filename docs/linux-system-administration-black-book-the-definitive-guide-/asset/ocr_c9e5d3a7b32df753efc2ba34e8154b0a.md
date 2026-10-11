![](bbox=[0.13, 0.08, 0.78, 0.42])

Figure 12.13 The Linuxconf Mail Queue dialog box.

# Configuring procmail

To configure **procmail** as a local mailer, do the following on each machine for which you want to use **procmail** for local mail handling:

+   1. Log in as *root*.
+   2. Type "`vi /etc/procmailrc`" to create and open the **procmail** configuration file for editing.

> **NOTE:** *This is the master **procmail** configuration file. Users can override its features for their own configuration in the `~/.procmailrc` file.*

+   3. Type "`i`" to enter Insert mode.
+   4. Although you can mix and match all the pieces in a **procmailrc** file if you want to, this example uses a set order to keep things clear. Many environment variables are available that you can set to your requirements. Choose the mail-specific environment variables you want to change, listed in Table 12.14.

> **TIP:** *To see what the values for any environment variables are set to, type `"echo $VARIABLE"`.*

+   5. Choose the logging-related environment variables you want to change. These variables are listed in Table 12.15.