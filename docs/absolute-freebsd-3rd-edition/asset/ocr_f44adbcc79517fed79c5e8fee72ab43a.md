# ## User's Home Directory

The ninth field is the user’s home directory. While this defaults to `/home/<username>`, you can move this anywhere appropriate. You’ll also need to move the actual home directory and its files when you change this field. Users with a nonexistent home directory can’t log in by default, although the `requirehome` setting in `login.conf` can change this.

# ## User's Shell

The final field is the user’s shell. If this field is empty, the system assigns the user the boring old `/bin/sh`.

While chpass(1) lets you muck up individual user accounts, vipw(8) unleashes you on the entire userbase. Be careful with it!

# ## Removing a User

The ruser(8) program deletes user accounts. You’ll be prompted for the username you want to delete and asked whether you want to remove that user’s home directory. That’s really all you have to do; destruction is much easier than creation, after all.

# ## Scripting with pw(8)

The pw(8) command provides a powerful command line interface to user accounts. While useradd(8) walks you through setting up an account in a friendly manner, pw(8) lets you specify everything on a single command line. I find pw(8) cumbersome for day-to-day use, but if you manage many user accounts, it’s invaluable.

One thing I do use pw(8) for is locking accounts. While a locked account is active, nobody can log in to it. I’ve used this to great effect when a client was behind on a bill; users call quite quickly when they can’t log in, and yet their websites continue to come up and their email continues to accumulate.

```
# pw lock xistence
```