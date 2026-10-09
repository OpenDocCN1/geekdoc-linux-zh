
## User Management and $EDITOR

User management tools such as chpass and vipw (as well as many other system management tools) bring up a text editor window where you make your changes. These tools generally check the environment variable $EDITOR to see which text editor you prefer. $EDITOR lets you default to vi, Emacs, or any other editor installed. I recommend Vigor, a vi(1) clone with an animated-paperclip help system that might make users of older Microsoft Office versions feel more comfortable.

### Changing Accounts with chpass(1)

The account has more information associated with it than just the password. The chpass(1) utility lets users edit everything they can reach in their account. For example, if I run chpass(1) as a regular user, I get an editor with the following text:

```text
#Changing user information for mwlucas.
Shell: /bin/tcsh
Full Name: Michael W Lucas
Office Location:
Office Phone:
Home Phone:
Other Information:
```

I'm allowed to edit six informational fields in my account. The first, my shell, can be set to any shell listed in /etc/shells (see “Shells and /etc/shell” on page 178). I can change my full name; perhaps I want my full middle name listed, or maybe I wish to be known to other system users as Mr. Scabies. I can update my office location and office phone so my coworkers can find me easily. This is another feature that was very useful on the university campuses where BSD grew up and where system users rarely had an idea of anyone's physical location. Now that we have extensive online directories and many more computers, it's less useful. I generally set my home phone number to 911 (999 in the UK), and I put a little bit of personal information in the other space.

Also note what I *can't* change as a regular user. The sysadmin sets my home directory, and I may not change it even if the system has a new hard drive with lots of empty space for my MP3 collection. My UID and GID numbers, similarly, are assigned by the system or the sysadmin.

On the other hand, if I run chpass xistence, its heightened privileges give me a very different view.

```text
#Changing user information for xistence.
Login: xistence
Password: $6$D9b4FfD0kHKHk2sPSP$bxUFTQqv/QposXw2KTLwszvpvz4HBo8...
Uid [#: 1001
Gid [# or name]: 1001
Change [month day year]:
Expire [month day year]:
Class:
Home directory: /home/xistence
Shell: /bin/csh
Full Name: Bert Regeer
Office Location:
Office Phone:
Home Phone:
Other information:
```

As root, you can do anything you like to the poor user. Changing his login to *megalos* is only the start of the havoc you can wreak. You even get access to the user's hashed password. Don't alter this field, unless you're comfortable computing password hashes. Use *passwd(1)* to more safely and reliably change the user's password. You can also change the user's home directory, although chpass(1) doesn't move the user's files; you must copy them by hand.

You can also set a date for password changes and account expiration. Password expiration is useful if you've just changed a user's password and you want him to change it upon his first login. Account expiration is useful when someone asks for an account but insists it's needed only for a limited time. You can forget to go back to delete that account, but FreeBSD never forgets. Both of these fields take a date in the form *month day year*, but you need only the first three letters of the month. For example, to make a user's password expire on June 8, 2028, I would enter Jun 8 2028 in the change space. Once the user changes his password, the password expiration field is blanked out again, but only the system administrator can extend an account expiration date.

## The Big Hammer: vipw(8)

While chpass(1) is fine for editing individual accounts, what happens when you must edit many accounts? Suppose your system has hundreds of users and a brand new hard disk for the home partition. Do you really want to run chpass(1) hundreds of times? That's where vipw(8) comes in.

Directly edit /etc/master.passwd with vipw(8). When you finish your edits, vipw(8) checks the password file's syntax to be sure you haven't ruined anything. Then, it saves the new password file and runs pwd_mkdb(8). Although vipw(8) can protect your password file from many basic mistakes, if you're clever, you can still muck things up. You must understand the format of the password file to use vipw(8) properly.

If the information in /etc/master.passwd conflicts with information in other files, /etc/master.passwd wins. For example, the primary group that appears in /etc/master.passwd is correct, even if /etc/group doesn't show the user as a member. This “master.passwd is always correct” logic is deeply ingrained throughout user management.

Each line in /etc/master.passwd is a single account record, containing 10 colon-separated fields. These fields are the following:

### Username

This field is either an account name created by the sysadmin or a username created at install time to provide some system service. FreeBSD includes users for system administration, such as root, daemon, games, and so on. Each of these users owns a part of the base system. FreeBSD also provides accounts for common services, such as the www user reserved for use by web servers. Add-on software might add its own system accounts as well.

### Encrypted Password

The second field is the encrypted password. System users don't have a password, so you can't log in as one of them. User accounts have a string of random-looking characters here.

### User ID

The third field is the *user ID number*, or UID. Every user has a unique UID.

### Group ID

Similarly, the fourth field is the *group ID number*, or GID. This is the user's primary group. Usually this is identical to the UID, and the group has the same name as the username.

### User's Class

The next field is the user's class as defined in /etc/login.conf (see "Restricting System Usage" on page 188).

### Password Expiration

This field is the same as the password expiration date set via chpass(1), but here the time gets stored as seconds from the epoch. Use date -j and the +%s output format to generate epochal seconds from a real date. To convert midnight, June 1, 2018, to epochal seconds, run `date -j 201806010000 '+%s'`.

### Account Expiration

This field enables you to make the account shut itself off on a certain day. Just set the account expiration date as you would for password expiration.

### Personal Data

This field is also known as the *gecos* field for obscure historical reasons. It contains the user's real name, office number, work phone number, and home phone number, all separated by commas. Do not use colons in this field; /etc/master.passwd reserves colons as a field delimiter.

### User's Home Directory

The ninth field is the user’s home directory. While this defaults to `/home/<username>`, you can move this anywhere appropriate. You’ll also need to move the actual home directory and its files when you change this field. Users with a nonexistent home directory can’t log in by default, although the `requirehome` setting in `login.conf` can change this.

### User's Shell

The final field is the user’s shell. If this field is empty, the system assigns the user the boring old `/bin/sh`.

While chpass(1) lets you muck up individual user accounts, vipw(8) unleashes you on the entire userbase. Be careful with it!

## Removing a User

The ruser(8) program deletes user accounts. You’ll be prompted for the username you want to delete and asked whether you want to remove that user’s home directory. That’s really all you have to do; destruction is much easier than creation, after all.

## Scripting with pw(8)

The pw(8) command provides a powerful command line interface to user accounts. While useradd(8) walks you through setting up an account in a friendly manner, pw(8) lets you specify everything on a single command line. I find pw(8) cumbersome for day-to-day use, but if you manage many user accounts, it’s invaluable.

One thing I do use pw(8) for is locking accounts. While a locked account is active, nobody can log in to it. I’ve used this to great effect when a client was behind on a bill; users call quite quickly when they can’t log in, and yet their websites continue to come up and their email continues to accumulate.

```bash
# pw lock xistence
```
