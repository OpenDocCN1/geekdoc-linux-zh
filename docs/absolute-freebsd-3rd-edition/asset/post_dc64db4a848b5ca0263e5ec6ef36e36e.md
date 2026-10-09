
## adduser

❶ Username: xistence  
❷ Full name: Bert Reger  
❸ Uid (Leave empty for default):  

The username ❶ is the name of the account. Users on my systems get a username of their first initial, middle initial, and last name. You can assign usernames by whatever scheme you dream up. Here, I let the user pick their own username, an indulgence I always later regret. The full name ❷ is the user’s real name. FreeBSD then lets you choose a numerical user ID (UID) ❸. FreeBSD starts numbering UIDs at 1,000; while you can change this, all UIDs below 1,000 are reserved for system use. I recommend just pressing ENTER to take the next available UID.

❶ Login group [xistence]:  
❷ Login group is xistence. Invite xistence into other groups? []: www  
❸ Login class [default]:  
❹ Shell (sh csh tcsh nologin) [sh]: tcsh  
❺ Home directory [/home/xistence]:  
❻ Home directory permissions (Leave empty for default):  

The user’s default group ❶ is important—remember, Unix permissions are set by owner and group. The FreeBSD default of having each user in their own group is usually the most sensible way for most setups. Any of the big thick books on system administration offers several grouping schemes—feel free to use whatever matches your needs. You can add this user to other groups ❷ in addition to the primary group at this time, if appropriate.

A login class ❸ specifies what level of resources the user has access to. We’ll talk about login classes later in this section.

The shell ❹ is the command line environment. While the system default is /bin/sh, I prefer tcsh. 1 If you’re deeply attached to another shell, feel free to use it instead. Knowledgeable users can change their own shells.

The home directory 5 is where the user's files reside on disk. The user and that user's primary group own this directory. You can set custom permissions 6 on the directory if you want, probably so that other users can't view this user's directory.

1. Use password-based authentication? [yes]:  
2. Use an empty password? (yes/no) [no]:  
3. Use a random password? (yes/no) [no]: y  
4. Lock out the account after creation? [no]: n  

The password options give you a certain degree of flexibility. If all of your users are comfortable with key-based SSH authentication, perhaps you can get away without using passwords. In the meantime, the rest of us are stuck with passwords 1.

Use an empty password 2 if you want the user to set his or her own password via the console. Whoever connects to that account first gets to set the password. This makes an empty password a good idea right up there with smoking inside a hydrogen dirigible.

A random password 3, on the other hand, is a good idea for a new account. The random password generator FreeBSD provides is good enough for day-to-day use. Random passwords are usually hard to remember, which encourages the user to change his password as soon as possible.

When an account is locked 4, nobody can use it to log in. This is generally counterproductive.

After entering all this information, adduser spits everything back at you for review and confirmation or rejection. Once you confirm, adduser verifies the account setup and provides you with the randomly generated password. It then creates the user's home directory, copies the shell configuration files from /etc/skel, and asks whether you want to set up another user.

### Configuring Adduser: /etc/adduser.conf

Creating new users on some Unix systems requires you to manually edit /etc/passwd, rebuild the password database, edit /etc/group, create a home directory, set permissions on that home directory, install dotfiles, and so on. This makes handling your local customizations routine—if you set everything by hand, you can manage your local account setup easily. The adduser(8) program provides a set of sensible defaults. For sites with different requirements, /etc/adduser.conf lets you set those requirements as defaults while retaining the high degree of automation. To create adduser.conf file, run adduser -c and answer the questions.

1. Uid (Leave empty for default):  
2. Login group []:  
3. Enter additional groups []: staff  
4. Login class [default]: staff  
5. Shell (sh csh tcsh nologin) [sh]: tcsh  
6. Home directory [/home/]: /nfs/u1/home  
7. Use password-based authentication? [yes]:  
8. Use an empty password? (yes/no) [no]:  
9. Use a random password? (yes/no) [no]: yes  
10. Lock out the account after creation? [no]: no  

You might want to start numbering UIDs somewhere other than 1,000. If you want higher initial UIDs, enter it in the uid space 1. Don't start below 1,000.

The login group 2 is the default user group. An empty login group means the user account defaults to having its own unique user group (the FreeBSD default).

You can specify any additional user groups 3 that new accounts belong to by default, as well as the login class 4. I set both of these to staff so that all new users get added to that group and assigned that class.

Choose a default shell 5 for your users.

Your home directory location 6 might vary from the standalone FreeBSD standard. In this example, I've specified a typical style of NFS-mounted home directories used when many users have accounts on many machines.

Choose the default password behavior for new users. You can specify whether users should use passwords at all 7 and whether the initial password should be empty 8 or random 9. Finally, dictate whether new accounts should default to being locked or not 10. You’ll find more configuration settings in adduser.conf(5). While you can set account characteristics here, the format of this file is considered internal to adduser(8). The setting names can change with any FreeBSD release. To change adduser.conf, re-run adduser -c.

### Editing Users

Managing users isn’t just about creating and deleting accounts. You’ll need to change those accounts from time to time. While FreeBSD includes several tools for editing accounts, the simplest are passwd(1), chpass(1), vipw(8), and pw(8). These work on the tightly interrelated files /etc/master.passwd, /etc/passwd, /etc/spwd.db, and /etc/pwd.db. We’ll start with the files and then review the common tools for editing those files.

The files /etc/master.passwd, /etc/passwd, /etc/spwd.db, and /etc/pwd.db hold user account information. Each file has a slightly different format and purpose. The file /etc/master.passwd is the authoritative source of user account information and includes user passwords in encrypted form. Normal users don’t have permission to view the contents of /etc/master.passwd. Regular users need access to basic account information, however; how else can unprivileged system programs identify users? The file /etc/passwd lists user accounts with all privileged information (such as the encrypted password) removed. Anyone can view the contents of /etc/passwd to get basic account information.

Many programs need account information, and parsing a text file is notoriously slow. In this day of laptop supercomputers, the word slow isn’t very meaningful, but this was a very real problem back when disco freely roamed the earth. For that reason, BSD-derived systems build a database file out of /etc/master.passwd and /etc/passwd. (Other Unix-like systems have similar functionality in different files.) The file `/etc/spwd.db` is taken directly from `/etc/master.passwd` and contains sensitive user information, but it can be read only by root. The file `/etc/pwd.db` can be read by anyone, but it contains the limited subset of information contained in `/etc/passwd`.

Any time any standard user management program changes the account information in `/etc/master.passwd`, FreeBSD runs `pwd_mkdb(8)` to update the other three files. For example, the three programs `passwd(1)`, `chpass(1)`, and `vipw(8)` all allow you to make changes to the master password file, and all three programs trigger `pwd_mkdb` to update the related files.

### Changing a Password

Use `passwd(1)` to change passwords. A user can change his own password, and root can change anyone’s password. To change your own password, just enter `passwd` at the command prompt.

```
# passwd
Changing local password for mwlucas
Old Password:
New Password:
Retype New Password:
```

When changing your own password, `passwd(1)` first asks for your current password. This is to ensure that nobody else can change your password without your knowledge. It’s always good to log out when you walk away from your terminal, but when you don’t, this simple check in `passwd(1)` prevents practical jokers from really annoying you. Then enter your new password twice, and it’s done. When you’re the superuser and want to change another user’s password, just give the username as an argument to `passwd`.

```
# passwd mwlucas
Changing local password for mwlucas
New Password:
Retype New Password:
```

Note that root doesn’t need to know the user’s old password; the root user can change any user account on the system in any manner desired.
