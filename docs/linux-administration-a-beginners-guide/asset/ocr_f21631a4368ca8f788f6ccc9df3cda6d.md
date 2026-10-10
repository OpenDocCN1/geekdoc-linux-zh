other way in which to read or manipulate user information is through a series of API calls.

In contrast, Linux takes the path of traditional UNIX and keeps all user information in straight text files. This is beneficial for the simple reason that it allows you to make changes to user information without the need of any other tool but a text editor such as pico. In many instances, larger sites take advantage of these text files by developing their own user administration tools so that they can not only create new accounts but also au- tomatically make additions to the corporate phone book, Web pages, and so on.

Users and groups working with UNIX style for the first time, however, may prefer to stick with the basic user management tools that come with the Linux distribution. We'll discuss those tools later in this chapter. For now, let's examine how Linux's text files are structured.

# The /etc/passwd File

The /etc/passwd file stores the user's login, encrypted password entry, user ID (UID), de- fault group ID (GID), name (sometimes called GECOS), home directory, and login shell.

The file keeps one user per line, and each entry for the user is delimited by a colon. For example:

```
sssh:boQavVhf4CkAxg:100:102::/svee Shash:/usr/sash:/bin/csh
```

In general, the login should not exceed eight characters. This is especially true if you are working in a heterogeneous UNIX environment, since different UNIXs handle lon- ger login names in different ways.

We discussed the details of the passwd entry earlier in this chapter. In the code lis- ting above, you can actually see what a DES encrypted password looks like (the informa- tion following the first column). Many sites disable accounts by altering the encrypted password entry so that when the disabled account's user enters his password, it won't match the value in the passwd file. (The guaranteed method of altering passwords for this reason is to insert an asterisk (*) into the entry. The above entry, for example, could be altered to boQavVhf4CkAxg*.)

> TIP: When disabling accounts in this manner, you may find it helpful not only to add a asterisk char- acter, but to add a star to indicate why the account was disabled in the first place. For example, if you catch a user downloading pirated software, you could disable his account by changing the encrypted entry to boGAVhf4Ck2xg*caught pirating.

The user ID (UID) must be unique for every user, with the exception of the UID zero. Any user who has a UID of zero has root (administrative) access and thus has full run of the system. Usually, the only user who has this specific UID has the login "root." It is con- sidered bad practice to allow any other users or user names to have a UID of zero. This is notably different from the Windows NT model, in which any number of users can have Administrative privileges.