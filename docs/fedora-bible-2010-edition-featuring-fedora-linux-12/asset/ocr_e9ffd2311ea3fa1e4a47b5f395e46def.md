| Option | Description |
| --- | --- |
| -M | Does not create the new user's home directory, even if the default behavior is set to create it. |
| -N | Turns off the default behavior of creating a new group that matches the name and user ID of the new user. |
| -o | Uses -u uid to create a user account that has the same UID as another user name. (This effectively lets you have two different users with authority over the same set of files and directories.) |
| -p passwd | Enters a password for the account you are adding. This must be an encrypted password. Instead of adding an encrypted password here, you can simply use the passwd user command later to add a password for user. The user should be asked to change immediately the password you set. |
| -r | Allows you to create a new account with a user ID in the range reserved for system accounts. |
| -s shell | Specify the command shell to use for this account. Replace shell with the command shell. |
| -u user_id | Specify the user ID number for the account. The default behavior is to assign the next available number automatically. Replace user_id with the ID number. |
| -U | Create a group with the same name as the user and add the user to that group. Normally, this is the default action. |
| -Z SELinuxUser | Define the SELinux user for the new user's login. If a user is not specified, the system picks the default SELinux user. |

As an example, create an account for a new user named John Smith with a login name of jsmith. First, log in as root, and then type the following command:

```
# useradd -c "John Smith" -m jsmith
```

> **TIP:** When you choose a user name, don't begin with a number (for example, 06smith). Also, it is best to use all lowercase letters; no control characters, tabs, special characters, or spaces; and a maximum of eight characters. The useradd command allows up to 32 characters, but some applications can't deal with user names that long. Tools such as ps display UIDs instead of names if names are too long. Having users named Jsmith and jsmith can cause confusion with programs (such as sendmail) that don't distinguish by case. Also, some very old applications may not be able to handle user names with more than eight characters.

Next, set John's initial password using the passwd command. The passwd command prompts you to type the password twice. (Asterisks are shown here to represent the password you type. Nothing is actually displayed when you type the password.)

```
# passwd jsmith
```