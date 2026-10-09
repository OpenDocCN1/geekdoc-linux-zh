It is common to forward mail sent to many special accounts to **root**. If Zach is to read mail sent and forwarded to **root**, you could fix each alias individually. Alternatively, you can simply add the following line *to the end* of the **aliases** file (order does matter in this case). This line forwards to Zach all mail sent and forwarded to **root**:

```
```
...  
root:          zach
```
```

You can create simple mailing lists with this type of alias. For example, the following alias sends copies of all email sent to **admin** on the local system to several users, including Zach, who is on a different system:

```
```
admin:        sam, helen, max, zach@example.com
```
```

You can direct email to a file by specifying an absolute pathname in place of a destination address. The following alias, which is quite popular among less conscientious system administrators, redirects email sent to **complaints** to /dev/null (page 503), where it disappears:

```
```
complaints:      /dev/null
```
```

You can also send email to standard input of a command by preceding the command with the pipeline character (|). This technique is commonly used by mailing list software such as Mailman (page 762). For each list it maintains, Mailman has entries, such as the following one for **painting_class**, in the aliases file:

```
```python
painting_class:  "|/var/lib/mailman/mail/mailman post painting_class"
```
```

# **newaliases**  

After you edit /etc/aliases, you must either run **newaliases** while you are working with **root** privileges or restart **sendmail** to re-create the /etc/aliases.db file that **sendmail** reads.

# **praliases**  

You can use **praliases** to list aliases currently loaded by **sendmail**:

```
```
# praliases | head -5
@: @
abuse: root
adm: root
amanda: root
daemon: root
```
```

# ~/.forward

Systemwide aliases are useful in many cases, but **nontroot** users cannot make or change them. Sometimes you might want to forward your own mail: Maybe you want mail from several systems to go to one address, or perhaps you want to forward your mail while you are working at another office. The ~/.forward file allows ordinary users to forward their email.

Lines in a .forward file are the same as the right column of the aliases file explained earlier in this section: Destinations are listed one per line and can be a local user, a remote email address, a filename, or a command preceded by the pipeline character (|). Mail that you forward does not go to your local mailbox. If you want to forward mail and keep a copy in your local mailbox, you must specify your local username preceded