If you get an error message when using the option `uaux`, then the other variant of `ps` is installed. You have to use the option `-ef` instead to get a similar output, but this version does not allow the easy sorting of processes based on their CPU usage. Another use of `ps` is to determine how many processes of a certain program are running. This can be accomplished by chaining the output of `ps` to other commands at the users’ disposal. To find out how many processes sendmail has spawned, for example, one possible chain of commands could be as shown in Listing 1.17.

# **LISTING 1.17**  Count of Running sendmail Processes

```
root@unixhost:> /usr/ucb/ps uaux | grep sendmail | wc -l
3
```

It seems that there are three running sendmail processes. To verify that this result is correct, starting the command without relaying the output to `wc`, thus omitting the `| wc -l` part, displays the found number of lines for inspection (see Listing 1.18).

# **LISTING 1.18**  Displaying Executing sendmail Processes

```
root@unixhost:> /usr/ucb/ps uaux | grep sendmail
root      740  0.1  0.6  992  696  pts/5    S 11:57:03  0:00 grep
sendmail
smsm      592  0.0  1.2 4352 1448  ?        S 10:07:08  0:00 /usr/lib/
sendmail -Ac -q15m
root      593  0.0  1.7 4384 2000  ?        S 10:07:08  0:00 /usr/lib/
sendmail -bd -q15m
```

This command line reveals there are actually *two* running sendmail processes. `grep` listed itself because the string `sendmail` is part of the command as well. To make use of the count, the line containing `grep` has to be eliminated from the list that is relayed to `wc`. There is more than one way to achieve this; option one, see Listing 1.19, is a commonly used choice.

# **LISTING 1.19**  Suppressing the Display of Lines Containing grep

```
root@unixhost:> /usr/ucb/ps uaux | grep sendmail | grep -v grep
smsm      592  0.0  1.2 4352 1448  ?        S 10:07:08  0:00 /usr/lib/
sendmail -Ac -q15m
root      593  0.0  1.7 4384 2000  ?        S 10:07:08  0:00 /usr/lib/
sendmail -bd -q15m
```