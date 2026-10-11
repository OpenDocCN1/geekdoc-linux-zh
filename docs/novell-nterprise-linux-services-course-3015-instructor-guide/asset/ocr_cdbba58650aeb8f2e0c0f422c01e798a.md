Depending on which agents you have running on your messaging system, the message might be checked against a system blacklist, forwarded to another email address, or filtered according to user-defined rules.

The file system structure used for message processing is comprised of 3 directories:

+   - Message Store
+   - Single Copy Message Store
+   - Message Queue

Everything that happens from the time a message enters the messaging system to when it is delivered to the user’s mailbox occurs in these directories.

# ### Message Store

The message store is the directory structure that holds users’ mailboxes and messages. All other information required by your NetMail system is stored in eDirectory. Every server running an NMAP Agent has a message store.

On a Linux server, the default message store location is /var/opt/novell/netmail/users. This location, of course, can be changed using WebAdmin.

The NMAP Agent creates the following mailbox directory structure within the message store directory for every User object in its assigned contexts:

Table 8-2

| Directory | Function |
| :--- | :--- |
| .users | Collective directory for all user mailboxes. |