Note that after both the first and second failed attempts to login to the system we “start over.” The system recognizes the invalid user name on the first attempt and the invalid password on the second attempt and in both cases supplies a “Login incorrect” message and starts over. The “Login incorrect” message is intentionally ambiguous, so you don’t know whether your user name, password, or both are incorrect; therefore as little information as possible is give to someone attempting unauthorized access to the system.

After the successful login, you are given information about the system, your terminal, and any other information the system administrator thinks would be useful to you. This information surely differs on your system.

After login we want to proceed to issue commands. In this example, first command we’ll issue is to change the temporary password supplied to us by the system administrator. You may find that after your first login you are *required* to change your password. The **passwd** command is used to change the password. Let’s issue the **passwd** command and try to change our password to the current password, that is, no change. Then let’s try to change the password to *passwd*. Finally, we’ll change the password to a valid password:

![](bbox=[0.87, 0.36, 0.97, 0.5])

```
martyp $ passwd
passwd: Changing password for martyp
Enter login password:
New password:                 <-- change to current password
passwd (SYSTEM): Password cannot be circular shift of loginid.
New password:                 <-- change to passwd
passwd (SYSTEM): The first 6 characters of the password
must contain at least two alphabetic characters and at least
one numeric or special character.
New password:                 <-- change to valid password
Re-enter new password:
passwd (SYSTEM): passwd successfully changed for martyp
martyp $
```

When we try to change the password to the current password, which is the same as our user name, we are told that the password can’t be a “circular shift of loginid.” This means that the login name and the password on this system must differ substantially. When we