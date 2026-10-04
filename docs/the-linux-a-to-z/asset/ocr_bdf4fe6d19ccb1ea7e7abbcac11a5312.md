**password** This is the user's password. Don't be surprised if you don't recognize yours. This is quite correct as the passwords are encrypted. When you enter your password on login it will be encrypted in the same way and compared with this field to allow or deny system access. If this field is empty then no password is required for this user.

**uid** Once logged in, the system refers to a user by a *user identity number* (uid) and not by the login name. This is where the uids are allocated.

**gid** Sometimes, a team of users will want to be able to work together in a group on a single project. For this, it would be useful to allow them common access to particular directories and files. This is done by allocating all the members of the team the same gid (*group identity number*) in this field.

**comment** This is just a comment field. It is commonly used to hold the user's real name and other personal details.

**home** This field specifies the absolute pathname to the user's home directory, which the system picks up on login.

**shell** This is the absolute pathname to a command that will be executed when any successful login is made on this user name. This can be any command, but for an ordinary user account it will be the pathname of a shell. If no pathname is given then this defaults to /bin/sh.

Because the password encryption algorithm is deemed to be so secure, the password file (/etc/passwd) is made publicly readable. However, if you choose a simple word as a password, such as you might find in a dictionary, then it is a simple matter to encrypt all the words in the dictionary to see if one matches.

There are two ways to overcome this problem. One is to make the encrypted passwords private, and there are packages available for Linux to do just that. In these packages the encrypted passwords are removed and stored in a separate file (typically /etc/shadow) to which public read access is denied. Having an extra file available also allows the addition of more fields to a user's record to specify such things as how often the users must change passwords. The other way to overcome the problem is much simpler and equally effective – choose a good password to start with. A good password will be at least six characters long and contain a mix of upper and lower case letters, digits and/or punctuation characters. If that sounds as though it will be hard to remember then make it a simple word, but change some of the characters in it to others that are visually similar (e.g. shelter and 5he!tER). This technique will give a much more secure password, though a more sophisticated password cracking program might still be able to find it.

For maximum security it is also advisable to change your password from time to time. Changing passwords under Linux is easy – you just enter the command:

```
$ passwd
```

and the system will prompt you for your old password, if you have one, and then prompt you twice for your new one. You have to enter the new password twice because the system does not echo the passwords you type so you don't see them