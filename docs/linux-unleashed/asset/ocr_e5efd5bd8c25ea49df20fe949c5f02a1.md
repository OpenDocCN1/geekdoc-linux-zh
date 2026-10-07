# Wildcards: * and ?

In many a late-night card game, jokers are shuffled into the deck. The jokers are *wild-cards* that can become any card of your choice. This is obviously very useful! Linux also has wildeards. They are more useful than jokers in a card game.

Linux has several wildcards. Wildcards are used as a convenient and powerful shortcut when specifying files (or directories) that a command is to operate on. We will briefly look at the two most popular wildcards: * and ?. (There are quite a few more wildcards supported by Linux, but they are seldom used and would only complicate the issue at this point.)

The most commonly used wildcard is *, which stands in for any combination of one or more characters. For example, `c*` matches all filenames that begin with c. You can see this for yourself by typing `ls /bin/c*`. What happens if you type `ls /bin/c**t` at the command line? How about `ls /bin/*t` at the command line?

The ? wildcard is more restrictive than *. It stands in only for any *one* character. You can see this by comparing `ls/bin/d*` with `ls/bin/d?`.

> NOTE
Wildcards can only be used to match filenames and directory names. You can't, for example, type `pass*` at the Linux prompt and expect Linux to run the `passwd` program for you.

> WARNING
Be very careful when using wildcards with dangerous commands, such as the ones used to permanently delete files! A good check is to run `ls` with the wild-cards you plan to use and examine the resulting list of files to see whether the wildcard combination did what you expected it to do. Also double-check that you typed everything correctly *before* pressing the Enter key!

# Environment Variables

When you log in, Linux keeps a number of useful data items in the background ready for the system to use. The actual data is held in something called an *environment variable*, whose name is often descriptive or mnemonic. In fact, this is no different from the way