> The passwd command asks for the password twice, but it does not echo what you type. This prevents somebody who sees your screen from reading the password. passwd is described in more detail shortly, in “Setting a Password.”

# Modifying User Accounts

User accounts may be modified in many ways: You can directly edit critical files such as `/etc/passwd`, modify user-specific configuration files in the account’s home directory, or use system utilities like those used to create accounts. You usually modify an existing user’s account at the user’s request or to implement some new policy or system change, such as moving home directories to a new hard disk. Sometimes, though, you must modify an account immediately after its creation in order to customize it in ways that aren’t easily handled through the account-creation tools or because you realize you forgot a parameter to `useradd`.

# Setting a Password

Although `useradd` provides the `-p` parameter to set a password, this tool isn’t very useful when directly adding a user because it requires a pre-encrypted password. Therefore, it’s usually easiest to create an account in disabled form (by not using `-p` with `useradd`) and set the password after creating the account. You can do this with the `passwd` command, which has the following syntax:

```
passwd [-k] [-l] [-u [-f]] [-d] [-S] [username]
```

> Although passwd is frequently used to set or change passwords, some of its actions don’t prompt you for a password. Instead, they modify the password in predictable ways, as described shortly. Other uses produce a password prompt at which you must type a new password (twice, to guard against typos).

The parameters to this command enable you to modify its behavior:

+   * **Update expired accounts** The `-k` parameter indicates that the system should update an expired account.
+   * **Lock accounts** The `-l` parameter locks an account by prefixing the encrypted password with an exclamation mark (!). The result is that the user can no longer log into the account, but the files are still available and the change can be easily undone. This parameter is particularly handy if you want to temporarily suspend user access to an account—say, because you’ve spotted some suspicious activity involving the account or because you know a user won’t be using the account for a while and you want to minimize the chance of it being abused in the interim.