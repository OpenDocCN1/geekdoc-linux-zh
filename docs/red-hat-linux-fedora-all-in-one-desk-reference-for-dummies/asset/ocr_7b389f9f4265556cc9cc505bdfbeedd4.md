With procmail, you can perform other chores, such as automatically storing messages in a file or forwarding messages to others. All you have to do is create an appropriate .procmailrc file in your home directory. To learn more about procmail, type man procmail. To see examples of .procmailrc, type man procmailrex.

# The sendmail alias file

In addition to the sendmail.cf file, sendmail also consults an alias file named /etc/aliases to convert a name into an address. The location of the alias file appears in the sendmail configuration file.

Each alias is typically a shorter name for an e-mail address. The system administrator uses the sendmail alias file to forward mail, to create mailing lists (a single alias that identifies several users), or to refer to a user by several different names. For example, here are some typical aliases:

```
barkakati: naba
naba: naba@inbsoft
all: naba, leha, ivy, emily, ashley
```

The first line says that mail addressed to barkakati should be delivered to the user named naba on the local system. The second line indicates that mail for naba should really be sent to the username naba on the inbsoft system. The last line defines all as the alias for the five users naba, leha, ivy, emily, and ashley. That means mail sent to all would go to these five users.

![](bbox=[0.13, 0.65, 0.2, 0.78])

After defining any new aliases in the /etc/aliases file, you must log in as root and make the new alias active by typing the following command:

```
sendmail -bi
```

# Installing the News Server

If you install the news server during Red Hat Linux installation, you don't have to do much more to begin using the news services. Otherwise, you can use the Red Hat Package Manager (RPM) to install the InterNetNews (INN) — a TCP/IP-based news server.

To check whether INN is already installed, type the following command:

```
rpm -q inn
```

If INN is installed, you should see a line similar to this:

```
inn-2.3.5-4
```