+   - **Email will be deleted from inboxes after a specific period**—This prevents users from bypassing home directory disk quotas and storing files in their email inbox.
+   - **Once an email is read, it is automatically moved to another location**—Many users will read an email message and mark it as unread. Some email systems will allow you to automatically move email to another location once a user has read it.
+   - **If an inbox exceeds a specific size, it will be archived**—This policy is useful in organizations where deletion or movement of email to a user’s home directory are not viable options. In many organizations, users may abandon their accounts, but the administrator may not have the options to delete the user. If the user was a member of mailing lists, their inbox could become quite large. By archiving the inbox, email resources are conserved, and no email is deleted.

# INBOX BACKUP

One final policy to consider is if and how you choose to back up your users’ email in their inboxes. Current legal precedents have shown that email is similar to other corporate documents in that a user’s email correspondence can be used as evidence during legal proceedings. If you work in a corporation that is concerned about legal risks, you may consider not backing up your email inbox filesystem.

There is a good reason for not backing up inboxes. Some users may feel that once a message is deleted from their inbox, it is gone forever. However, if you as the administrator had backed up that user’s inbox, the message will still exist on your backup media. If the authorities seize your corporate records, you as the administrator may be asked to hand over all of your backup media so the authorities can scan your backups for evidence. For this reason, it is important to be sure that your user knows a message is deleted when they delete it from their inbox.

# Summary

There are three basic agents used to handle the flow of email: the Mail Transfer Agent (MTA), the Mail Delivery Agent (MDA), and the Mail User Agent (MUA). To successfully interact, these three agents must conform to standard protocols. The IETF administers the official Internet protocol standards for electronic mail. In this chapter we briefly explained these agents