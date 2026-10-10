cracker’s pre-encrypted dictionary from the previous paragraph is blown up by a factor of 4096.

![](bbox=[0.31, 0.11, 0.35, 0.14])

Nowadays, password encryption is commonly based on the MD5 algorithm, allows for passwords of arbitrary length and uses a 48-bit salt instead of the traditional 12 bits. Kindly enough, the encryption works much more slowly than “crypt”, which is irrelevant for the usual purpose (checking a password upon login—you can still encrypt several hundred passwords per second) but does encumber clever crackers to a certain extent. (You should not let yourself be bothered by the fact that cryptographers poo-poo the MD5 scheme as such due to its insecurity. As far as password encryption is concerned, this is quite meaningless.)

![](bbox=[0.31, 0.25, 0.35, 0.28])

You should not expect too much of the various password administration parameters. They are being used by the text console login process, but whether other parts of the system (such as the graphical login screen) pay them any notice depends on your setup. Nor is there usually an advantage in forcing new passwords on users at short intervals—this usually results in a sequence like bob1, bob2, bob3, ..., or users alternate between two passwords. *A minimal interval that must pass before a user is allowed to change their password again is outright dangerous, since it may give a cracker a “window” for illicit access even though the user knows their password has been compromised.*

The problem you need to cope with as a system administrator is usually not people trying to crack your system’s passwords by “brute force”. It is much more promising, as a rule, to use “social engineering”. To guess your password, the clever cracker does not start at a, b, and so on, but with your spouse’s first name, your kids’ first names, your car’s plate number, your dog’s birthday et cetera. (We do not in any way mean to imply that *you* would use such a stupid password. No, no, not *you* by any means. However, you are not quite so positive about your boss ...) And then there is of course the time-honoured phone call approach: “Hi, this is the IT department. We’re doing a security systems test and urgently require your user name and password.”

There are diverse ways of making Linux passwords more secure. Apart from the improved encryption scheme mentioned above, which by now is used by default by most Linux distributions, these include complaining about (too) weak passwords when they are first set up, or proactively running software that will try to identify weak encrypted passwords, just like clever crackers would. (*Caution: Do this in your workplace only with written (!) pre-approval from your boss!)* Other methods avoid passwords completely in favour of constantly changing magic numbers (as in SecurID) or smart cards. All of this is beyond the scope of this manual, and therefore we refer you to the Linup Front manual *Linux Security*.

# 13.3.3 The /etc/group File

By default, Linux keeps group information in the */etc/group* file. This file contains one-line entry for each group in the system, which like the entries in */etc/passwd* consists of fields separated by colons (`:`). More precisely, */etc/group* contains four fields per line.

```
```
(group name)::{password}::{GID}::{members}
```
```

Their meaning is as follows:

(*group name*)  The name of the group, for use in directory listings, etc.

(*password*)  An optional password for this group. This lets users who are not members of the group via */etc/shadow* or */etc/group* assume membership of the group using *newgr*. A "*" as an invalid character prevents normal users