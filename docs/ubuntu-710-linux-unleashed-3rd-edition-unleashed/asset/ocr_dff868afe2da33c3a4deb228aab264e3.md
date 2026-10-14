his special shell, and the -u option to specify her UID. (If we create a user with the default settings, we do not need to use these options.) All we want to do can be accomplished on one line:

```
$ sudo useradd bernice -p Sticher -s /bin/zsh -u 1002
```

The sysadmin can also use the graphical interface that Ubuntu provides, as shown in Figure 10.2. It is accessed as the Users and Groups item from the Administration menu. Here, the sysadmin is adding a new user to the system where user bernice uses the bash command shell.

These are the steps we used to add the same account as shown in the preceding command, but using the graphical User Manager interface:

+   1. Launch the Ubuntu User Manager graphical interface by clicking on the Users and Groups menu item found in the System Settings menu.
+   2. Click the Add User button to bring up the Add User dialog window.
+   3. Fill in the form with the appropriate information as requested, ensuring you create a good password.
+   4. Click the Advanced tab and open the drop-down Shell menu to select the bash shell.
+   5. Using the arrows found in the UID dialog, increment the UID to 1413.
+   6. Click OK to save the settings.

Note that the user is being manually assigned the UID of 1413 because that is her UID on another system machine that will be connected to this machine. Because the system only knows her as 1001 and not as bernice, the two machines would not recognize bernice as the same user if two different UIDs were assigned.

> **NOTE**
> 
> A Linux username can be any alphanumeric combination that does not begin with a special character reserved for shell script use (see Chapter 11 for disallowed characters, mostly punctuation characters). In Chapter 4, we told you that usernames are typically the user’s first name plus the first initial of her last name. That is a common practice on larger systems with many users because it makes life simpler for the sysadmin, but is neither a rule nor a requirement.

# Monitoring User Activity on the System

Monitoring user activity is part of the sysadmin’s duties and an essential task in tracking how system resources are being used. The w command tells the sysadmin who is logged in, where he is logged in, and what he is doing. No one can hide from the super user. The w command can be followed by a specific user’s name to show only that user.