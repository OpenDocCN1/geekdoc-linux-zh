You can also give the name of the command you wish to reissue. Let’s say that you want to reissue the last **fc** command. You would simply give the letter "f" along with the **r** command, and the last command that started with **f** would be reissued, as shown in the following example:

```
```text
marty p $ history
308    history -5
309    history
310    pwd
311    whoami
312    pwd
313    cat /etc/profile
314    ls
315    fc -l
316    env
317    who
318    cat /etc/passwd
319    ls -al
320    history
321    more .profile
322    set
323    history
marty p $ r f
fc -l
309    history
310    pwd
311    whoami
312    pwd
313    cat /etc/profile
314    ls
315    fc -l
316    env
317    who
318    cat /etc/passwd
319    ls -al
320    history
321    more .profile
322    set
323    history
324    fc -l
marty p $
```
```

![](bbox=[0.88, 0.81, 0.96, 0.9])

You can also perform some substitution with the **r** command. If you issued the **vi** command earlier and want to rerun **vi** but specify a different file name to edit, you can substitute a new file name. The fol-