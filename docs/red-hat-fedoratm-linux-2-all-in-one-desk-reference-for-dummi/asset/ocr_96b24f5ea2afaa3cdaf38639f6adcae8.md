3. Log in as root and set up a symbolic link in /etc/smsh to the /usr/bin/procmail program with the following command:
`ln -s /usr/bin/procmail /etc/smsh/procmail`

This step is necessary because sendmail uses the SendMail Restricted Shell — smsh — to run external programs. Instead of running /usr/bin/procmail, smsh runs /etc/smsh/procmail. That’s why you need the symbolic link. This link is a security feature of sendmail that controls what external programs it can run.

That’s it! Now, if you receive any messages from an address containing mailing_list, the message is deleted.

With procmail, you can perform other chores, such as automatically storing messages in a file or forwarding messages to others. All you have to do is create an appropriate .procmailrc file in your home directory. To find out more about procmail, type man procmail. To see examples of .procmailrc, type man procmailex.

# The sendmail alias file

In addition to the sendmail.cf file, sendmail also consults an alias file named /etc/aliases to convert a name into an address. The location of the alias file appears in the sendmail configuration file.

Each alias is typically a shorter name for an e-mail address. The system administrator uses the sendmail alias file to forward mail, to create mailing lists (a single alias that identifies several users), or to refer to a user by several different names. For example, here are some typical aliases:

```
```
barkakati: naba
naba: naba@lnbsoft
all: naba, leha, ivy, emily, ashley
```
```

The first line says that mail addressed to barkakati is delivered to the user named naba on the local system. The second line indicates that mail for naba really is sent to the username naba on the lnbsoft system. The last line defines all as the alias for the five users naba, leha, ivy, emily, and ashley. That means mail sent to all goes to these five users.

![](bbox=[0.13, 0.82, 0.22, 0.88])

After defining any new aliases in the /etc/aliases file, you must log in as root and make the new alias active by typing the following command:
`sendmail -bf`