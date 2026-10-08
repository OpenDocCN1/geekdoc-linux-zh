The following example will not allow mail to be sent to **cyberspammer.com** (a recipient), nor can mail be received for **justin@lizard.mytrek.com**, **secretproject@rabbit.mytrek.com**, or **mysurfbboard.com**:

```
```
mysurfbboard.com                      ERROR: "Domain does not exist"
justin@lizard.mytrek.com              "Moved to Hawaii"
secretproject@rabbit.mytrek.com       REJECT
cyberspammer.com                     REJECT
```
```

Your distribution version of **smb.conf** may configure Sendmail to use **access_db** (as is the case with Fedora). Access is granted only to users on the local host. If your system is being used as a mail server for a network and you have not enabled the **relay_entire_domain** feature, you will need to allow access by other hosts on your network. In the access file, you can place a **RELAY** rule for your network. The **RELAY** rule will let other hosts use your mail server to send messages out to other hosts. This is normally done for a gateway host that needs to relay messages from a local network out to the Internet. The following example allows access from the **mytrek.com** network:

```
```
mytrek.com            RELAY
```
```

For a specific host, place an entry for it in the access file as shown here:

```
```
rabbit.mytrek.com       RELAY
```
```

To further secure Sendmail, you should disable the use of **VRFY**. This option allows remote users to try to verify the existence of a user address. This can be used to guess valid users on your system. This option is disabled with the **noverify** feature:

```
```
FEATURE('noverify')dn1
```
```

Another potential security breach is the **EXPn** option, which expands mailing lists and aliases to their actual addresses. Use the **noexpxn** feature to turn it off:

```
```
FEATURE('noexpxn')dn1
```
```

By default, Sendmail will refuse mail from any domain that cannot be resolved. You can override this restriction with the **accept_unresolvable_domains** feature. Sendmail will also reject mail whose addresses do not have fully qualified domain names. You can override this feature with **accept_unqualified_senders**.

# ## POP and IMAP Server: Dovecot

The protocols Internet Mail Access Protocol (IMAP) and Post Office Protocol (POP) allow a remote server to hold mail for users who can then fetch their mail from it when they are ready. Unlike procmail, which delivers mail messages directly to a user account on a Linux system, the IMAP and POP protocols hold mail until a user accesses an account on the IMAP or POP server. The servers then transfer any received messages to the user’s local mailbox. Such servers are often used by ISPs to provide Internet mail services for users. Instead of being sent directly to a user’s machine, the mail resides in the IMAP or POP