
## Managing Your User Accounts

### User Account Passwords (the /etc/shadow File)

As it happens, any user has read access to the /etc/passwd file – indeed, this access is handy if, say, you need to match an account name to its UID. But as we mentioned above, older versions of Linux stored account passwords in encrypted format in the second field of the /etc/passwd file. A consequence of this was that it was easy for users to access the encrypted versions of the passwords of other users.

Initially, this was not considered a security issue because the passwords were encrypted. However, the storage of encrypted passwords in /etc/passwd is no longer considered safe; as we'll see in a moment, techniques now exist that make it much easier to guess a user's password given its encrypted form and knowledge of the encryption algorithm.

To plug this security hole, Red Hat Linux 9 stores encrypted passwords in a different file – /etc/shadow. This file is accessible to root only. While normal users can still read from /etc/passwd, they do not have permission to read from /etc/shadow, and thus do not have access to encrypted passwords.

### Password Encryption

While the account passwords are now stored safely in the restricted access /etc/shadow file, Red Hat Linux still takes the precaution of storing them in encrypted format.

Let's see what an encrypted password looks like. If you use root privileges to examine the contents of the /etc/shadow file, you'd see each encrypted password stored as an incomprehensible string of characters like this:

`$1$mWzQxxFuT$EWhSix5hmxiiERbUpEwR5V0`

Red Hat Linux never stores passwords in the clear text form in which the user enters them. Rather, it always encrypts them before storing them or working with them, in such a way that it is not easily possible (or even feasible) to decipher the encrypted version and find out the original.

In fact, once the password has been encrypted and stored in /etc/shadow, there will never be the need to decrypt it ever again. This is a key point: when a user logs in, the operating system verifies their identity by encrypting the submitted password and comparing it with the encrypted string contained in the /etc/shadow. If the two strings match, access is granted. It is this process that enables Red Hat Linux to avoid ever having to decrypt passwords.

### A Technique for Guessing Passwords

Unfortunately, the fact that a password is encrypted before storage is not enough to guarantee that it can't be discovered by other means. While it's very difficult to use decryption techniques to discover the original passwords, it is quite possible to use a brute force method to find out "weak" passwords. The power of modern computer hardware makes it possible to take large numbers of common passwords, encrypt them using the same algorithm used by the operating system, and check if the encrypted version is the same as the one stored in the password file.

This technique is often called a dictionary attack, because the attacker can take large numbers of candidate passwords from a dictionary. A surprising number of passwords can be cracked in this way – indeed, in Chapter 12 we'll take a look at a program called crack, which uses this technique to crack passwords.

The existence of such techniques is the motivating factor behind the decision to place passwords in /etc/shadow, rather than /etc/passwd. Thus, users are prevented from stealing encrypted passwords, and then trying to "break" the weak ones via a dictionary attack.

*Further discussion of cryptographic techniques is outside of the scope of this chapter. However, cryptography is a fascinating science. If you're interested, you could start experimenting with GnuPG (the GNU Privacy Guard) – install the gnupg package on your system, then have a look at the gpg command. The gpg manual page will certainly be useful, providing information and lists of other documents.*

### A Sample /etc/shadow File

Let's examine a few lines from a sample /etc/shadow file. This example contains the entries for the accounts we used via the User Manager, earlier in this chapter. Once again, your /etc/shadow will probably differ from this, although its structure will be similar:

```text
root:$1$eÂuê€ûAÊ$Kv55YoAiHDcPli1gq1Go:11961:0:99999:7:::
halt:*:11961:0:99999:7:::
eziodm:$1$W/RgbXrIOSOP9t9IyVmQyvPfxNLUFWQl:12100:0:99999:7:::
kapils:!!$1$68Q7Ci4g$CqbN8rdoCBw4GmxDlouQ2q/:12100:0:99999:7:::
deepak:$1$sUeJrHGf$J3cSo2TRmKTbN55wFLgfeb1:12100:0:99999:7:::
```

Just like /etc/passwd, each line (or record) represents a user, and adjacent fields are separated by " : ". Again, to understand the purpose of the fields in this file, let's look at the third line:

![](img/b852150740856958b10aff9e8c9d2adc_307_0.png)

- The first field contains the account name. It must match the name found in /etc/passwd.
- The second field contains the encrypted password. A * character here indicates that the account is disabled (that is, the user cannot log in), while a !! sequence here (followed by the original encrypted password) indicates that the account is temporarily locked.
- The third field indicates the date when the password was last changed. It is expressed as the number of days elapsed since January 1, 1970. It is very typical, in systems of Unix descent, to count the number of days or seconds since this date. In the example above, we can see that eziodm's password was last changed 12100 days after January 1, 1970.
- The fourth field contains a count of the number of days before the password *may* next be changed. The value zero or an empty field (as in the examples above) means that it can be changed anytime.
- The fifth field contains a count of the number of days after which the password *must* be changed. This default value means that the password can stay in its place for almost 274 years, which is probably long enough!
- The sixth field specifies how many days warning the user will get that their password is about to expire.
- The seventh field specifies after how many days the account is disabled if its owner does not change the password when requested to.
- The eighth field is the date when the account will be unconditionally disabled, expressed in days since January 1, 1970.
- Finally, at the end of the line there is one more empty field, reserved for future use.

To get more information about `/etc/shadow`, you can consult its manual page, by typing `man 5 shadow` at your shell prompt.

## Groups (the /etc/group File)

A user can belong to many groups, but as we've seen, `/etc/passwd` allows only membership of one group (the **primary group**). Membership of additional groups must be specified in the `/etc/group` file. Unsurprisingly, this file is very similar in structure to the two we've already seen. The following example shows the groups we created earlier in this chapter:

```text
root:x:0:root
bin:x:1:root,bin,daemon
daemon:x:2:root,bin,daemon
eziodm:x:500:
kapis:x:501:
deepakt:x:502:
authors:x:503:eziodm,kapils,deepakt
```

The structure is quite simple. Let's study the second line of this file to understand the fields:

![](img/b852150740856958b10aff9e8c9d2adc_309_0.png)

- The first field contains the group name.
- The second field contains a placeholder for an optional **group password**. The password, if present, is stored in `/etc/gshadow`. Group passwords are rarely used so we won't discuss them here.
- The third field contains the group identification number (GID). As we've mentioned, every group on the system must have its own unique GID. Recall that `/etc/passwd` refers to primary groups by number, not by name; so when it's necessary, this field is used to match a group number with its corresponding group name.
- The last field contains the **list of user accounts** that belong to this group.

For more information about `/etc/group`, you can type `man 5 group` at your shell prompt.

## Advanced User Account Management

We've also seen how to manage user accounts and groups via the Red Hat User Manager, and we've seen how Red Hat Linux stores this user information in the configuration files `/etc/passwd`, `/etc/shadow`, and `/etc/group`.

It's evident that these configuration files are just plain text files, and it's perhaps tempting to put aside the User Manager and edit those files manually, using a text editor such as `gedit`. It is quite possible to manage your user information this way, but it is safer to use the User Manager or the CLI commands instead:

- First, the files are of critical importance to the successful execution of your Red Hat Linux installation, and their integrity must be ensured at all times. The tools are designed to ensure the integrity of these files, but if you edit them manually then you are on your own.
