+   - **UID:** Each user needs a unique UID on the system. Select the UID for the new account using the policies you have defined for UID assignment as suggested earlier in the section “Selecting UIDs.”
+   - **GID:** Each user needs a default group as specified by a GID. Select the default group’s GID for the new account using the policies you have defined for group assignment as suggested earlier in the section “Selecting Groups.”
+   - **Full Name:** Each account can have a full name specified.
+   - **Home Directory:** Each account on the system needs a home directory. This is the default location where the user can create files and directories and keep personalized configuration files. Select a home directory for the account using the policies you defined as suggested earlier in the section “Where to Locate Home Directories.”
+   - **Default Shell:** Each account needs a default shell. The default shell indicates the command-line shell that will be launched when a user logs in. On most Linux systems the default shell is Bash, but you can choose any valid shell available on your system. You will need to specify the complete path of the shell’s binary executable file such as `/bin/bash` for Bash.

Using this information, you need to create a new entry for the account in the `/etc/passwd` file. As outlined earlier in the section “The `/etc/passwd` File,” entries in the password file take the following form:

```
<username>:<password>:<UID>:<GID>:<full name>:<home directory>:<default shell>
```

Leave the password field blank so a typical entry for a new account might look like the following:

```
someuser::501:501:A new user account:/home/someuser:/bin/bash
```

> > **Caution**
> > It is crucial that you do not edit the `/etc/passwd` file directly. As outlined earlier in the section “The `/etc/passwd` File,” use the `vipw` command to edit the `/etc/passwd` file.

After the entry is added to the account, assign an initial password to the account with the `passwd` command. For instance, to assign a password to the someuser account, use the following command:

```
# passwd someuser
Changing password for user someuser
New UNIX password:
Retype new UNIX password:
passwd: all authentication tokens updated successfully
```

The passwd command will encrypt the password and add it to the appropriate field in the account’s entry in the `/etc/passwd` file:

```
someuser:fog4fihy6UjI:501:501:A new user account:/home/someuser:/bin/bash
```