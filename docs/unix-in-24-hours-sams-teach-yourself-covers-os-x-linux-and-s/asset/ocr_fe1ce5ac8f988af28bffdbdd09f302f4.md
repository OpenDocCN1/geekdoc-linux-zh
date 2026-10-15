# Task 14.5: Setting Custom Prompts

Up to this point, the command prompt you’ve seen is a boring $. It turns out that bash lets you set your prompt to just about any possible value, with PS1="value". Note that PS1 must be all uppercase for this to work.

+   1. I’m getting tired of Unix being so blunt and impolite. Fortunately, I easily can change how it responds to me:

```
$ PS1="Yes, master? "
Yes, master?
```

That’s more like it!

+   2. There are a lot of things you can tuck away in your prompt that can be of great help, and they all take the form of \x. The first useful variable is \w, which holds the current working directory:

Click here to view code image

```
Yes, master? PS1="In \w, oh master: "
In /users/taylor, oh master:
```

What happens if I change directories?

Click here to view code image

```
In /users/taylor, oh master: cd /
In /, oh master:
```

Cool, eh?

+   3. There are a lot of different variables you can add, the most useful of which are shown in Table 14.2.

| Value | Expands to |
| --- | --- |
| \d | The date, in Weekday Month Day format (example: Thu Feb 1) |
| \H | The full system hostname (example: limbo.intuitive.com) |
| \h | The system name (example: limbo) |
| \n | Carriage return sequence (yes, you can have a two-line prompt, if you want!) |
| \s | The name of the shell (example: bash2.4) |
| \T | Current time, in HH:MM:SS format (example: 04:23:28) |
| \t | Same as \T, but in 24 hour format (example: 16:23:28) |
| \@ | Current time in am/pm format (example: 04:23pm) |
| \u | Username of the current user (example: taylor) |
| \w | Current working directory (example: /home/taylor/bin) |
| \W | Base name of current directory (example: bin) |

# TABLE 14.2 Special Values for the System Prompt

Remember how you learned earlier this hour about using the command numbers to repeat commands (like !37 to repeat command #37)? It turns out that there’s an