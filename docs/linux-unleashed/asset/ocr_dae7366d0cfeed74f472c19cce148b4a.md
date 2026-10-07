The messages for the most part are the same as when you logged in as root. Some sys-tems don't show you anything except the shell prompt, but you can change that. Note that your prompt looks different from the root prompt or the pound sign. The $ prompt indicates that you are a regular user running under the bash shell (which was the default choice presented by the adduser program). Also, there is no You have mail message (because you have no mail).

![](bbox=[0.22, 0.26, 0.93, 0.35])

To see an example of the difference between the root login and a regular user login, type **adduser** at the shell prompt and press **Enter**.

```
```
darkstar:~$ adduser
bash: adduser: command not found
```
```

The message you get looks somewhat cryptic. However, it has a typical Linux error mes-sage structure, so it's worth making a little effort now to understand it.

# ## Linux Error Messages

First of all, in the error message shown previously there's quite a bit of information. The program that is giving you the message is your shell, *bash*. It therefore announces itself with *bash*:, somewhat like the character in a play script. Next is the shell's “mono-” “logo.” Being the “strong and silent” type of character, *bash*'s monologue is very terse and to the point. It declares the program that is causing problems (adduser) and the spe-cific problem with this program: the command (adduser) can't be found.

If the error message were expanded into real English, it would read something like this: “Hi, I'm *bash*. You know that adduser command you gave me? I looked everywhere for adduser but I couldn't find it, so I couldn't perform whatever actions adduser would have specified.” With time, you will get quite good at understanding Linux error mes-sage grammar.

# ## Search Paths

Why can root find adduser, but an ordinary user cannot? Linux has many directories, and each directory can hold many files (one of which can be the elusive adduser). In theory, Linux could go search through the entire file system until it found adduser. But if root accidentally mistyped adduser as asuser, Linux would have to rummage