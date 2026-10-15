
```
alias ll='ls -l'
alias ls='/bin/ls -F'
alias mail=Mail
alias mailq='/usr/lib/sendmail -bp'
alias newaliases='echo you mean newalias..'
alias rn='/usr/local/bin/rn -d$HOME -L -M =m -e -S -/'
alias intuitive='echo Intuitive.com; \
echo ''MyPassWord.'' | pbcopyssh dtaylor@intuitive.com'
```

Also notice that the shell always shows an alphabetically sorted list of aliases, regardless of the order in which they were defined.

Most of these aliases are easy to understand. For example, the first alias, diff, ensures that the command diff always has the default flags -c and -w. If I enter from, I want the system to invoke frm -n; if I enter ll, I want the system to invoke ls -l; and so on.

## 2. Some commands can cause trouble if entered, so creating an alias for each of those commands is a good way to stay out of trouble. For example, I have an alias for newaliases; if I accidentally enter that command, the system gently reminds me that I probably meant to use the newalias command:

```
$ newaliases
you mean newalias..
```

## 3. I have created aliases for connecting to accounts on other systems. I like to name each alias after the system to which I’m connecting (for example, intuitive):

Click here to view code image

```
$ alias intuitive
alias intuitive='echo Intuitive.com;echo ''MyPassWord.'' | pbcopyssh dtaylor@intuitive.com'
```

Separating commands with a semicolon is the Unix way of having multiple commands on a single line, so when I enter the alias sunworld, for example, it’s as if I’d entered all these commands one after another:

```
echo Intuitive.com
echo 'MyPassWord.' | pbcopy
ssh dtaylor@intuitive.com
```

> Before you get too excited, no, “MyPassWord.” is not my real account password!

Using aliases is a great way to really customize your command interface. I always tweak the set of commands and the default flags. (For example, look at all the options I set as default values for the rn command.) I even effectively disable commands that I don’t want to enter accidentally.

Let your imagination run wild with aliases! If you decide you really like one and you’re using bash, add the alias to your .bashrc file so that it’s permanent. (You can also put these into your .profile file if you prefer.) If you want to temporarily have the system “forget” an alias, you can use the unalias command, and it’s gone until you log in again. For example, unalias intuitive would temporarily remove from the shell the intuitive alias shown earlier.

## Task 14.5: Setting Custom Prompts

Up to this point, the command prompt you’ve seen is a boring $. It turns out that bash lets you set your prompt to just about any possible value, with PS1="value". Note that PS1 must be all uppercase for this to work.

- 1. I’m getting tired of Unix being so blunt and impolite. Fortunately, I easily can change how it responds to me:

```
$ PS1="Yes, master? "
Yes, master?
```

That’s more like it!

- 2. There are a lot of things you can tuck away in your prompt that can be of great help, and they all take the form of \x. The first useful variable is \w, which holds the current working directory:

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

- 3. There are a lot of different variables you can add, the most useful of which are shown in Table 14.2.

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

### TABLE 14.2 Special Values for the System Prompt

Remember how you learned earlier this hour about using the command numbers to repeat commands (like !37 to repeat command #37)? It turns out that there’s an
