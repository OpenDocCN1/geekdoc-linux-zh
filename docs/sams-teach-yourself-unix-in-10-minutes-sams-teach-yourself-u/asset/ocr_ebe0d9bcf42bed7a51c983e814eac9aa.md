How do I Read the Rest? When you see a ... on your screen, there's more text to be read. The man pages won't scroll automatically, so you'll need to press the Spacebar to see additional text. Press q to quit the page and return to the command line.

This is only a tiny subset of the information that is returned via the man command, but enough for you to get the picture. You'll soon find that using man pages to learn about everything that is available on your system is going to take a bit of time. You can speed things up by viewing a summary description of a command through one of four different commands: man -f, man -k, whatis, or apropos, followed by the name of the command you'd like to explore. Each of these functions returns similar results, but there are two different ways that the search is performed.

# man VARIATIONS, apropos, whatis

If you know the command you'd like to look up, use man -f, or whatis, followed by the command name.

For example, to print a summary for the date command, type:

```
>man -f date
 date (1)      - print or set the system date and time
END
```

A short description of what date does is returned. Press q to return to the command line.

If you're not quite sure what you're looking for, man -f and whatis search the description of each available command for matching keywords. If you experience any errors while running these commands it might be because the whatis database has been removed from your system, or has not been created. You'll need to contact your system administrator and ask her or him to use makewhatis to generate the database files necessary to use whatis. Because this is a function that affects protected areas of the system, it is not available to most users.

Now, try running whatis on the subject time. This turns up several relevant entries.