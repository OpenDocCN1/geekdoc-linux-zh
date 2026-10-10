Password-cracking programs work just like the login program, except that these programs pick one word at a time from a dictionary, encrypt the word, and compare the encrypted word with the encrypted passwords in the /etc/passwd file for a match. To crack the passwords, the intruder needs the /etc/passwd file. Often, crackers use weaknesses of various Internet servers (such as mail and FTP) to get a copy of the /etc/passwd file.

Several improvements have made passwords more secure in Linux. These include shadow passwords and pluggable authentication modules — described in the next two sections — and you can install these easily as you install Linux. During Linux installation, you typically get a chance to configure the authentication. If you enable MD5 password and enable shadow passwords, you automatically enable more secure passwords in Linux.

# Shadow passwords

Obviously, leaving passwords lying around where anyone can get at them — even if they're encrypted — is bad security. So instead of storing passwords in the /etc/passwd file (which any user can read), Linux now stores them in a shadow password file, /etc/shadow. Only the superuser (root) can read this file. For example, here is the entry for root in the new-style /etc/passwd file:

```
root::1:0:root:/root:/bin/bash
```

In this case, note that the second field contains an x instead of an encrypted password. The x is the shadow password; the actual encrypted password is now stored in the /etc/shadow file where the entry for root is like this:

```
root:$1$AAAnl/YH$UESKzX2bDyp9Cgf0o1BfO15O:11077:0:99999:7:-1:-1:134540356
```

The format of the /etc/shadow entries with colon-separated fields resembles the entries in the /etc/passwd file, but the meanings of most of the fields differ. The first field is still the username, and the second one is the encrypted password.

The remaining fields in each /etc/shadow entry control when the password expires. You don't have to interpret or change these entries in the /etc/shadow file. Instead, use the chage command to change the password-expiration information. For starters, you can check a user's password-expiration information by using the chage command with the -l option, as follows. (In this case, you have to be logged in as root.)

```
chage -l root
```

This command displays expiration information, including how long the password lasts and how often you can change the password.