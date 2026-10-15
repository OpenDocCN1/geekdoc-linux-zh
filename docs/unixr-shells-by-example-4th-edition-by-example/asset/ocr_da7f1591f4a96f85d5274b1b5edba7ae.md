# Table 11.6 Korn Shell Metacharacters (continued)

| Command | Function |
|---|---|
| [abc] | Match for one from a set of characters |
| [!abc] | Match for one not from the set of characters |
| * | Match for zero or more characters |
| (cmds ) | Execute commands in a subshell |
| {cmds} | Execute commands in current shell |

# EXAMPLE 11.26

```
1 $ ls -d s
all files are displayed
abc abc122 abc2 file1.bak file2.bak nonsense nothing one
abc1 abc123 file1 file2 none noone

2 $ print hello \
> there        # The carriage return is escaped
hello there

3 $ rusers&
# Process the rusers command in the background
[1] 4334
$

4 $ who; date; uptime   # Commands are executed one at a time
ellie console Feb 10 10:46
ellie tty p0 Feb 15 12:41
ellie tty p1 Feb 10 10:47
ellie tty p2 Feb 5 10:53
Mon Feb 15 17:16:43 PST 2004
5:16pm up 5 days, 6:32, 1 user, load average: 0.28, 0.23, 0.01

5 $ print $HOME        # The value of the HOME variable is printed
/home/jody/ellie

6 $ print $LOGNAME     # The value of the LOGNAME variable is printed
ellie

7 $ ( pwd; cd / ; pwd )
/home/jody/ellie
/
```