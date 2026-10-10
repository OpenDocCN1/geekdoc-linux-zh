
min The minimal number of days that must have passed since the last password change before the password may be changed again.

max The maximal number of days that a password remains valid without having to be changed. After this time has elapsed the user must change his password.

warn The number of days before the expiry of the (max) period that the user will be warned about having to change his password. Generally, the warning appears when logging in.

grace The number of days, counting from the expiry of the (max) period, after which the account will be locked if the user does not change his password. (During the time from the expiry of the (max) period and the expiry of this grace period the user may log in but must immediately change his password.)

lock The date on which the account will be definitively locked, again in days since 1 January 1970.

Some brief remarks concerning password encryption are in order. You might think that if passwords are encrypted they can also be decrypted again. This would open all of the system's accounts to a clever cracker who manages to obtain a copy of /etc/shadow. However, in reality this is not the case, since password "encryption" is a one-way street. It is impossible to recover the decrypted representation of a Linux password from the "encrypted" form because the method used for encryption prevents this. The only way to "crack" the encryption is by encrypting likely passwords and checking whether they match what is in /etc/shadow.

Let's assume you select the characters of your password from the 95 visible ASCII characters (uppercase and lowercase letters are distinguished). This means that there are 95 different one-character passwords, $95^{2}=9025$ two-character passwords, and so on. With eight characters you are already up to 6.6 quadrillion ($6.6 \cdot 10^{15}$) possibilities. Stipulating that you can trial-encrypt 250,000 passwords per second (not entirely unrealistic on current hardware), this means you would require approximately 841 years to work through all possible passwords.

But do not feel too safe yet. The traditional method (usually called "crypt" or "DES"—the latter because it is based on, but not identical to, the eponymous encryption method) should no longer be used if you can avoid it. It has the unpleasant property of only looking at the first eight characters of the entered password, and clever crackers can nowadays buy enough disk space to build a pre-encrypted cache of the 50 million (or so) most common passwords. To "crack" a password they only need to search their cache for the encrypted password, which can be done extremely quickly, and read off the corresponding clear-text password.

To make things even more laborious, when a newly entered password is encrypted the system traditionally adds a random element (the so-called "salt") which selects one of 4096 different possibilities for the encrypted password. The main purpose of the salt is to avoid random hits resulting from user X, for some reason or other, getting a peek at the content of /etc/shadow and noting that his encrypted password looks just like that of user Y (hence letting him log into user Y's account using his own clear-text password). For a pleasant side effect, the disk space required for the cracker’s pre-encrypted dictionary from the previous paragraph is blown up by a factor of 4096.

![](img/44bdd771e9c9b1353d2401c2892b2459_177_0.png)

Nowadays, password encryption is commonly based on the MD5 algorithm, allows for passwords of arbitrary length and uses a 48-bit salt instead of the traditional 12 bits. Kindly enough, the encryption works much more slowly than “crypt”, which is irrelevant for the usual purpose (checking a password upon login—you can still encrypt several hundred passwords per second) but does encumber clever crackers to a certain extent. (You should not let yourself be bothered by the fact that cryptographers poo-poo the MD5 scheme as such due to its insecurity. As far as password encryption is concerned, this is quite meaningless.)

![](img/44bdd771e9c9b1353d2401c2892b2459_177_1.png)

You should not expect too much of the various password administration parameters. They are being used by the text console login process, but whether other parts of the system (such as the graphical login screen) pay them any notice depends on your setup. Nor is there usually an advantage in forcing new passwords on users at short intervals—this usually results in a sequence like bob1, bob2, bob3, ..., or users alternate between two passwords. *A minimal interval that must pass before a user is allowed to change their password again is outright dangerous, since it may give a cracker a “window” for illicit access even though the user knows their password has been compromised.*

The problem you need to cope with as a system administrator is usually not people trying to crack your system’s passwords by “brute force”. It is much more promising, as a rule, to use “social engineering”. To guess your password, the clever cracker does not start at a, b, and so on, but with your spouse’s first name, your kids’ first names, your car’s plate number, your dog’s birthday et cetera. (We do not in any way mean to imply that *you* would use such a stupid password. No, no, not *you* by any means. However, you are not quite so positive about your boss ...) And then there is of course the time-honoured phone call approach: “Hi, this is the IT department. We’re doing a security systems test and urgently require your user name and password.”

There are diverse ways of making Linux passwords more secure. Apart from the improved encryption scheme mentioned above, which by now is used by default by most Linux distributions, these include complaining about (too) weak passwords when they are first set up, or proactively running software that will try to identify weak encrypted passwords, just like clever crackers would. (*Caution: Do this in your workplace only with written (!) pre-approval from your boss!*) Other methods avoid passwords completely in favour of constantly changing magic numbers (as in SecurID) or smart cards. All of this is beyond the scope of this manual, and therefore we refer you to the Linup Front manual *Linux Security*.

## 13.3.3 The /etc/group File

By default, Linux keeps group information in the */etc/group* file. This file contains one-line entry for each group in the system, which like the entries in */etc/passwd* consists of fields separated by colons (`:`). More precisely, */etc/group* contains four fields per line.

```
(group name)::password::GID::members
```

Their meaning is as follows:

- (*group name*) The name of the group, for use in directory listings, etc.
- (*password*) An optional password for this group. This lets users who are not members of the group via */etc/shadow* or */etc/group* assume membership of the group using *newgrp*. A "*" as an invalid character prevents normal users from changing to the group in question. A “x” refers to the separate password file /etc/gshadow.
- **(<GID>)** The group’s numerical group identifier.
- **(<Members>)** A comma-separated list of user names. This list contains all users who have this group as a secondary group, i.e., who are members of this group but have a different value in the GID field of their /etc/passwd entry. (Users with this group as their primary group may also be listed here but that is unnecessary.)

A /etc/group file could, for example, look like this:

```
root:x:0:root
bin:x:1:root,daemon
users:x:100:
project1:x:101:joe,sue
project2:x:102:bob
```

The entries for the root and bin groups are entries for administrative groups, similar to the system’s pseudo-user accounts. Many files are assigned to groups like this. The other groups contain user accounts. Like UIDs, GIDs are counted from a specific value, typically 100. For a valid entry, at least the first and third field (group name and GID) must be filled in. Such an entry assigns a GID (which might occur in a user’s primary GID field in /etc/passwd) a textual name.

The password and/or membership fields must only be filled in for groups that are assigned to users as secondary groups. The users listed in the membership list are not asked for a password when they want to change GIDs using the newgrp command. If an encrypted password is given, users without an entry in the membership list can authenticate using the password to assume membership of the group.

In practice, group passwords are hardly if ever used, as the administrative overhead barely justifies the benefits to be derived from them. On the one hand it is more convenient to assign the group directly to the users in question (since, from version 2.6 of the Linux kernel on, there is no limit to the number of secondary groups a user can join), and on the other hand a *single* password that must be known by *all* group members does not exactly make for bullet-proof security.

If you want to be safe, ensure that there is an asterisk (“*”) in every group password slot.

### 13.3.4 The /etc/gshadow File

As for the user database, there is a shadow password extension for the group database. The group passwords, which would otherwise be encrypted but readable for anyone in /etc/group (similar to /etc/passwd), are stored in the separate file /etc/gshadow. This also contains additional information about the group, for example the names of the group administrators who are entitled to add or remove members from the group.

## Exercises

- 13.5 [1] Which value will you find in the second column of the /etc/passwd file? Why do you find that value there?
- 13.6 [2] Switch to a text console (using, e. g., [Alt]+[F1]) and try logging in but enter your user name in uppercase letters. What happens?
