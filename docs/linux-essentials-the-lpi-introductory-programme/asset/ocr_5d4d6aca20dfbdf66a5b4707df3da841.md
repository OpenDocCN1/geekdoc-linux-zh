“real” name, etc. After the system is first installed, the file contains entries for most pseudo-users.

The entries in /etc/passwd have the following format:

```
(user name): (password): (UID): (GID): (GECOS): (home directory) : (shell)
```

(user name) This name should consist of lowercase letters and digits; the first character should be a letter. Unix systems often consider only the first eight characters—Linux does not have this limitation but in heterogeneous networks you should take it into account.

![](bbox=[0.35, 0.26, 0.39, 0.3])

Resist the temptation to use umlauts, punctuation and similar special characters in user names, even if the system lets you do so— not all tools that create new user accounts are picky, and you could of course edit /etc/passwd by hand. What seems to work splendidly at first glance may lead to problems elsewhere later.

![](bbox=[0.35, 0.35, 0.39, 0.39])

You should also stay away from user names consisting of only uppercase letters or only digits. The former may give their owners trouble logging in (see Exercise 13.6), the latter can lead to confusion, especially if the numerical user name does not equal the account's numerical UID. Commands such as “ls -l” will display the UID if there is no corresponding entry for it in /etc/passwd, and it is not exactly straightforward to tell UIDs from purely numerical user names in ls output.

(password) Traditionally, this field contains the user’s encrypted password. Today, most Linux distributions use “shadow passwords”; instead of storing the password in the publicly readable /etc/passwd file, it is stored in /etc/shadow which can only be accessed by the administrator and some privileged programs. In /etc/passwd, a “x” calls attention to this circumstance. Every user can avail himself of the passwd program to change his password.

(UID) The numerical user identifier—a number between 0 and 2^32 – 1. By convention, UIDs from 0 to 99 (inclusive) are reserved for the system, UIDs from 100 to 499 are for use by software packages if they need pseudo-user accounts. With most popular distributions, “real” users’ UIDs start from 500 (or 1000).

Precisely because the system differentiates between users not by name but by UID, the kernel treats two accounts as completely identical if they contain different user names but the same UID—at least as far as the access privileges are concerned. Commands that display a user name (e.g., “ls -l” or id) show the one used when the user logged in.

primary group (GID) The GID of the user's primary group after logging in.

![](bbox=[0.34, 0.77, 0.41, 0.81])

The Novell/SUSE distributions (among others) assign a single group such as users as the shared primary group of all users. This method is quite established as well as easy to understand.

![](bbox=[0.34, 0.83, 0.41, 0.87])

Many distributions, such as those by Red Hat or Debian GNU/Linux, create a new group whenever a new account is created, with the GID equaling the account’s UID. The idea behind this is to allow more sophisticated assignments of rights than with the approach that puts all users in the same group users. Consider the following situation: Jim (user name jim) is the personal assistant of CEO Sue (user name sue). In this capacity he sometimes needs to access files stored inside Sue’s home directory that other users should not be able to get at. The method used by Red Hat, Debian & co., “one group per user”, makes it straightforward to put user jim into group sue and to arrange for Sue’s