# Changing an Account Expiration date

If you need a temporary access on a system, you can set the expiry date of an account. The administrator can change the account expiration date so that the account is disabled on a set date. If you want to change the account expiration date of a user, run the following command:

```
```text
#usermod -e MM - DD-YYYY <username>
```
```

In the preceding command MM-DD-YYYY represents the month, day and year; two-digit year fields are also accepted.

Let's take an example where you want an account for user deven to be expired on March 1, 2010. You can use the following command for this purpose:

```
```text
usermod -e 03/01/10 deven
```
```

This command resets the account expiration date for the user deven to March 1, 2010.

# Changing Finger Information

If you want to have the information about users on a system, you can use the following finger command:

```
```text
#finger <username>
```
```

You can obtain the user's full name, office location, and phone number from the preceding finger command. For example, to get the user deven full name, terminal name, home directory type the finger command as follows:

```
```text
#finger -1 deven
```
```

The preceding command prints the terminal name, home directory, mail status, home phone number of the user deven.

The chfn command is used to change a user's finger information. To change finger information for deven, type the chfn command as follows:

```
```text
#chfn deven
```
```

If you not specified which information (whether Full name, Phone number or directory) you want to change, you'll be prompted for each field information for the user. At the prompt, you can enter the new information, or just press return to leave the field unchanged or enter the keyword "none" to make the field blank.

# Deleting Users

The userdel command is used to delete a user account. In order to delete previously created user, Mahendra, type the userdel command as follows:

```
```text
#userdel Mahendra
```
```