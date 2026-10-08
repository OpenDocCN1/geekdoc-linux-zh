```
297  cat /etc/passwd
298  cat /etc/passwd | grep donna
299  pwd
300  history
martyp $ cat /etc/profile | grep vi
```

![](bbox=[0.85, 0.09, 0.98, 0.18])

This changes *more* to **cat** on the command line.

To delete the word *more* without replacing it, we fetch line 286 and issue **dw**, as shown in the following example:

![](bbox=[0.85, 0.19, 0.98, 0.275])

```
martyp $ history
285  history
286  more /etc/profile | grep vi
287  who
288  whoami
289  who
290  ls -al
291  alias
292  pwd
293  ls -al /home
294  cat .profile
295  history
296  vi .profile
297  cat /etc/passwd
298  cat /etc/passwd | grep donna
299  pwd
300  history
martyp $ /etc/profile | grep vi
```

If we are unhappy with the most recent command issued we can undo the command by issuing **u**, which undoes the **dw** we used to remove *more* on the command line, as shown in the following exam-ple:

```
martyp $ history
285  history
286  more /etc/profile | grep vi
287  who
288  whoami
289  who
290  ls -al
291  alias
```