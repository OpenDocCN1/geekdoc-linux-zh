# Creating default user settings

The default settings for creating new users using useradd come from /etc/default/useradd. An example of this file is shown in Listing 5-2.

# Listing 5-2 An Example /etc/default/useradd File

```
# useradd defaults file
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
```

The following are explanations of the entries in this file:

+   - **GROUP=100.** Specifies that the default GID is 100. This value is used only when you disable (using the -n option) the default private group (the group with the same name as the new user). You can specify a group name instead of the numeric value, as well. The value you specify in this line must exist in /etc/group. You can change this value as follows:
+   
+   ```
+   useradd -D -g newsgroup name or GID
+   ```
+   where newsgroup name and GID are the proper values.
+   
+   - **HOME=/home.** Specifies the default top-level home directory for new users. For example, when you create a new user called joe, the default home directory is /home/joe. You can change this to fit your needs. Make sure that the directory already exists. You can change this value as follows:
+   
+   ```
+   useradd -D -d directory
+   ```
+   
+   - **INACTIVE=-1.** Specifies when (in days) the account will become inactive after the password expires. This is useful only if you are using shadow passwords. The default value of -1 states that accounts are never inactive. You can change this value as follows:
+   
+   ```
+   useradd -D -f number of days
+   ```