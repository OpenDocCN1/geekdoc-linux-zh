# Summary

It would really take an entire book (or two') to describe fully all the ins and outs of shell scripts. The main idea here, however, is that you use a lot of commands repetitively, you should make them into a command alias (if they're short) or drop them all into a shell script. In shell scripts, as in awk, $1 is the first argument, $2 the second, and so on.

This hour introduced you to many of the most powerful aspects of UNIX shells. Practice creating aliases and working with the history list to minimize your typing. Also, find a prompt you like and set it in your .cshrc or .profile (for csh and ksh, respectively) so it will be the default.

# Workshop

The Workshop summarizes the key terms you learned and poses some questions about the topics presented in this chapter. It also provides you with a preview of what you will learn in the next hour.

# Key Terms

**basename** The closest directory name. For example, the basename of /usr/home/taylor is taylor.

**command number** The unique number by which the shell indexes all commands. You can place this number in your prompt using \! and use it with the history mechanism as command-number.

# Questions

+   1. How do you tell the C that you want it to remember the last 30 commands during a session and to remember the last 10 commands across login sessions?
2. Assume that you get the following output from entering history:
```
1 ls -CF
2 who | grep dunalim
3 wc -l test
4 cat test
5 history
```\What would be the result of entering each of the following history commands?
```
f2 lw twh echo !
```
3. Some UNIX systems won't enable you to do the following. What danger do you see lurking in this alias?
```
alias who -a
```

![](bbox=[0.065, 0.893, 0.145, 0.966])