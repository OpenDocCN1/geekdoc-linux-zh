# Chapter 14 ◆ Working with the System 395

![](bbox=[0.181, 0.131, 0.818, 0.513])

**Figure 14-12:** The YaST DHCP server screen in SUSE 9.3

# # Automating Tasks

A useful maxit states that if you have to do something manually more than three times, it's time to find a way to do it automatically. If the thing you need to do manually is a complicated shell command, then maybe what you need is an alias or a shell script to automate its effect.

# # Shell Aliases

If you have long commands that you regularly type, a **bash alias** is a nice way of reducing the amount of typing and thinking you have to do. You can create aliases at the command line (for the current session only) or permanently in the file ~/.alias.

For example, if you want to be able to use the single letter command **b** as an alias for the command `ssh user@somemachine.mydomain.net`, you can type:

```
user@bible:~$ alias b='ssh user@somemachine.mydomain.net'
```