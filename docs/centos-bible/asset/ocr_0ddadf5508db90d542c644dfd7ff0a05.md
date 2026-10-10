TABLE 10-1	(continued)
| Option | Description |
| :--- | :--- |
| -p passwd | Enter a password for the account you are adding. This must be an encrypted password. Instead of adding an encrypted password here, you can simply use the passwd command later to add a password for the user. The user should be asked to immediately change the password you set. |
| -r | Allows you to create a new account with a user ID in the range reserved for system accounts. |
| -s shell | Specify the command shell to use for this account. Replace shell with the command shell. |
| -u user_id | Specify the user ID number for the account. The default behavior is to automatically assign the next available number. Replace user_id with the ID number. |

Next, set Robert's initial password using the passwd command. The passwd command prompts you to type the password twice. Asterisks are shown here to represent the password you type. Nothing is actually displayed when you type the password.

```
# passwd robert
Changing password for user robert.
New password: ******
Retype new password: ******
```

> CROSS-REF	Refer to Chapter 13 for tips on picking good passwords.

In creating the account for Robert, the useradd command performs several actions:

+   Reads the /etc/login.defs file to get default values to use when creating accounts.
+   Checks command-line parameters to find out which default values to override.
+   Creates a new user entry in the /etc/passwd and /etc/shadow files based on the default values and command-line parameters.
+   Creates any new group entries in the /etc/group file.
+   Creates a home directory based on the user's name and places it in the /home directory.
+   Ccopies any files located within the /etc/skel directory to the new home directory. This usually includes login and application start-up scripts.

The preceding example uses only two of the available useradd options. Most account settings are assigned using default values. Here's an example that uses a few more options:

```
# useradd -m -g users -G wheel,sales -s /bin/tcsh -c "Connie James" connie
```