> e-mails account/password pairs to an e-mail address surreptitiously, or worse!

The test to see whether there are any accounts without passwords is a bit more tricky, because we need to check not only the /etc/passwd file, but also the /etc/shadow file. The trick is that only root can access the /etc/shadow file in the first place, so this command will have to be run by root:

```
# cat /etc/passwd /etc/shadow | awk -F: 'length($2) < 1 { print $0 }'
#
```

No output. Phew! What a relief!

To make this more interesting, however, I'll create a new account and omit the password:

```
# cp /etc/passwd /etc/passwd.save
# echo "taylorsu::0:502:Dave as Superuser:/home/root:/bin/bash" >> ~/etc/passwd
```

![](bbox=[0.25, 0.73, 0.3, 0.83])

> The >> is a very dangerous command, so either don't do it at all, or do it very, very carefully. If you were to accidentally use > instead of >>, for example, you'd have just deleted your entire /etc/passwd file, which could have catastrophic results! That's why you can see that I'm also saving a copy of the /etc/passwd file as /etc/passwd.save, just in case....

Now running the zero-password test is more interesting:

```
# cat /etc/passwd /etc/shadow | awk -F: 'length($2) < 1 { print $0 }'
taylorsu::0:502:Dave as Superuser:/home/root:/bin/bash
```

Got it! How about checking for more than one UID 0 account?

```
# awk -F: '$3 == 0 { print $0 }' /etc/passwd
root:x:0:0:root:/bin/bash
taylorsu:0:502:Dave as Superuser:/home/root:/bin/bash
```

Good. That flagged it, too. To fix it, I'll use passwd to set the password for this account, and we're done with this task.

There are a number of ways that the /etc/passwd file can be analyzed and tested in an automated fashion, as we've seen in this first task. The most important thing isn't to come up with super-fancy analysis tools, but to do some sort of analysis frequently. If someone hacks into your system, they're not going to wave a flag or send you an e-mail message, so your vigilance with the accounts in the /etc/passwd file is critical!