the password contains too few different characters, Linux will give this reprimand: BAD PASSWORD: it does not contain enough DIFFERENT characters. If the password is too recognizable to the system as an average word, Linux will respond, BAD PASSWORD: it is based on a dictionary word. If root changes this password, the system will still accept the new password no matter what the user inputs, but it will have given the user fair warning. If a regular user, however, attempts to input a bad password or one that the system deems unacceptable, he or she will be unable to continue until an acceptable password is chosen.

# # Expiring and Locking Passwords

Linux also offers a feature that expires a user's password after a certain date. This feature of the usermod command allows you to modify variables in the /etc/passwd file. If you want to disable a certain account's password on a specific date, using usermod with the -e option will expire that account on that specific day.

If I wanted to expire the password for the user karen on the October 31, 2000, and then issue her a new password, I would type the following command:

```
usermod -e 10/31/00 karen
```

> **NOTE**
> 
> To function, this feature must have shadow passwords enabled. Information regarding the expiration of a user's password is not normally stored in the /etc/passwd file, but in the /etc/shadow file instead. Shadow passwords are the system passwords that are encrypted elsewhere and which no one other than root has access to read. Because the /etc/passwd file must be readable by different system processes, such as bash for determining a user's home directory, the encrypted password text is also readable and thus dechiperable. By placing the encrypted text in another file, i.e. /etc/shadow, and changing the permission to 400, only root can then see what the encrypted password text might be.

The usermode e- feature is useful for users who are prone to reset their passwords to something easy. Expiring the passwords at a given time or after a certain number of days forces users to change their password again.

Along with using the -e option, you can also lock or disable an account by using -L with the usermod command to lock an account, or use this option's counterpart, the -u option, to unlock the same account. The -L option places an