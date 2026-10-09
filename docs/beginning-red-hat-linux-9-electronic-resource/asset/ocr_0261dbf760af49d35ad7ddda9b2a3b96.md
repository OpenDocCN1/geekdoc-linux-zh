To change the login shell, you can use the `chsh` command – which works in a very similar way:

```
$ chsh
Changing shell for eziodm.
Password: (password not shown)
New shell [/bin/bash]: /bin/tcsh
Shell changed.
```

If you want to return to your previous shell, just run `chsh` again and specify the original one:

```
$ chsh
Changing shell for eziodm.
Password: (password not shown)
New shell [/bin/tcsh]: /bin/bash
Shell changed.
```

You can find out more about `chfn` and `chsh` by consulting their manuals from a terminal with `man chfn` and `man chsh`.

# Using the root Account to Modify Another User Account

When we need to adopt the root account and apply changes to another account, the best tool to use is dependent on the changes we need to make. Some of the more *common* operations (like account or password expiry) are easy to perform, using the **Red Hat User Manager** (we select the account and then press the **Properties** button).

However, if we need to make more major changes to an account (such as changing the UID), the **Red Hat User Manager** is not enough. In fact, we can't even use the CLI-based commands like `passwd`, `chfn`, and `chsh` utilities to change the UID of an account.

If you absolutely *must* change an account home directory, UID, GID, or even login name, here's how to do it using `usermod` on the command line. Remember, you have to be logged in as root to do this! Let's suppose we have the following user in `/etc/passwd`:

```
eziodm:x:500:500:Pancrazio 'Ezio' de Mauro::/home/eziodm:/bin/bash
```

If we want to rename the account from `eziodm` to `eziod`, we can run `usermod` like this:

```
# usermod -l eziod eziodm
```

We've used the `-1` option to indicate that we want to change the login name, and we specify the *new* login name before the existing one. As a result, the record for this user in `/etc/passwd` changes to:

```
eziod:x:500:500:Pancrazio 'Ezio' de Mauro:/home/eziodm:/bin/bash
```