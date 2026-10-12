exclamation point (!) in front of the encrypted text of the password. This disables the password entirely so that the user cannot log in.

Here is how you would lock and then unlock the account of the user joe:

```
```
usermod -L joe
usermod -U joe
```
```

Naturally, you can use the usermod command only when acting as root. Because this command actually modifies the /etc/passwd file, which controls all user settings (or modifies the /etc/shadow file, depending on which function is enabled), strict limits are in place to prevent anyone other than root from changing user settings. Normal users do not have the proper permissions to modify their own accounts. The only exception to this rule is the ability to change their password

# Encrypting Passwords

I often receive calls from users requesting that I reset or change their passwords. Either they had forgotten the existing password or they had entered a password into their modem connection box and someone else had changed the asterisks so that their connection no longer worked. Many had difficulty believing that their passwords were encrypted. The best anyone can do in such a case is reset the password either to something similar or to something entirely different if it had been shared or compromised.

The fact that Linux encrypts all the passwords is an extremely good thing. It used to be that the encrypted text was kept in /etc/passwd file along with other user information. This was not good. The permissions on /etc/passwd are set at 644 and, as such, the entire file can be read with any text editor such as vi, or the cat command can be used against it and the file contents piped over into a separate file, as in cat /etc/passwd > passwords.txt. If a password-cracking program is run against that new file, before long the usernames along with their respective passwords are simple text once again. Realizing that this was not a good thing, the Linux developers took their cue from other more mature UNIX systems such as Solaris and created an /etc/shadow file. The permissions here are set at 400, meaning that only root (as the owner of the file) could read the contents. The /etc/shadow file stores all encrypted passwords. This affords the Linux system a double layer of security. Along with more restrictive file permissions, Red Hat provides MD5 hashing of the passwords within the /etc/passwd file, which adds another level of security, after which it is encrypted with libc's