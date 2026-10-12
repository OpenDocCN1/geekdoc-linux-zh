```
```
if [ "$ATYPE" = "b" ]; then     mail $1 < /usr/sbin/guide_dial-up.txtxt
fi
echo
echo "Setup complete."
echo

# End of file
```
```

You will recognize many of the useradd options from the previous chapters. This script creates an account for the user. It prompts the administrator for input, such as a username, which it then checks against the /etc/passwd file to see whether another user has already taken that name. If the username is available, the script then prompts for the user’s full name and finally the group to which to assign that user. After gathering the necessary information, the script employs the useradd command and enters all the information gathered. Finally, the script assigns quotas to the user’s account and sends the user a text e-mail explaining some basic functions.

A script like this takes care of some of the features that that you would ordinarily have to handle manually. It also showcases other distinctive innovations in Linux such as allocating the users to a particular group based on the type of account they requested and sending them an email with appropriate instructions.

The script in Listing 6.2 assists in manually deleting any rogue accounts. It is much shorter since, as you will discover when using Linux, it is much easier to delete files than to create them. Like the script in Listing 6.1, this script also has a short name that briefly describes its function. The name, however, is the script’s least important aspect. You can change the name to whatever best describes it or suits its purpose.

# Listing 6.2 A Simple Script for Removing Users from the System

```
```
#!/bin/bash
# dlu - a simple script for deleting users.
#print out the info for the user editing the account
if [ -z "$1" ]; then
echo "usage: dlu <username>"
```
```