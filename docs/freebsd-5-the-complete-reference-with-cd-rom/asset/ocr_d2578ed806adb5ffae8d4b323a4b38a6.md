![](bbox=[0.11, 0.13, 0.89, 0.29])

# ## User vs. root Accounts

As described in Chapter 2, you're likely to use at least two FreeBSD accounts: an ordinary user account and the root account. You employ a user account for day-to-day user tasks, such as reading e-mail, browsing the Web, using a spreadsheet, and manipulating graphics files. The root account is the account used by the system administrator, aka the *superuser*. This account provides more-or-less unlimited control of the computer; root can read, write, move, or delete any file on the system. For most tasks, you should use an ordinary user account; reserve root logins for the times when you need to administer the system.

> In this book, commands you type are shown after a prompt. In most cases, this prompt is either a dollar sign ($) or a pound sign (#), signifying the command's use from a user account or as root, respectively. This mirrors the default prompts displayed on the screen when you're logged in as an ordinary user or as root.

It's not uncommon to find that you've logged in as an ordinary user, but need superuser privileges for some short action. This problem can be overcome in several ways. One is to use FreeBSD's virtual consoles to log in as root, perform whatever action you need to do, and log out again. A procedure can be awkward if you're running in X and want to run a program that requires root privileges alongside other programs, though. Even when running in text mode, there's a method that's often simpler: su.

The su program name stands for substitute user. It's a method of changing the identity of a user who's already logged in. It can take several options and parameters:

```
su [-] [-f|-fm] [-c class] [username [args]]
```

> FreeBSD documentation often lists command syntax as in this example. Square brackets indicate a parameter that's optional. Single-character options within brackets can be added or deleted individually (as in -f|-fm in this example; you can use just -f, just -l, just -m, or any combination you like). Italic indicates variables. Ellipses (not shown here) indicate that an option may be repeated. A vertical bar (|, also not shown here) separates two alternatives that aren't used together.