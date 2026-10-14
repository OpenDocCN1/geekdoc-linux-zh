Finally, return to the primary Sendmail page, and click the Start Sendmail button. It is usually useful to keep an eye on the logs when starting a daemon so that problems will be immediately obvious. Sendmail logs to the mail log on most systems, which is likely located in /var/log directory. You can use the Webmin System Logs module to view this log.

# Tutorial: Virtual Hosting Email with Sendmail

Virtual hosting is a rather broad term applied to many network services to specify that the server in question provides service to two or more network domains with some degree of separation. Specifically, in the case of a mail server, it means that the mail server will deliver to a unique local user based on the username and the domain in the to field of the received email. For example, an email sent to joe@swelltech.com would be treated differently from an email sent to joe@notswelltech.com and would be delivered to a different mailbox.

As with most Open Source software there are many ways to accomplish our goal, but here you’ll learn the simplest method provided by Sendmail. Configuring Sendmail for virtual mail hosting is a three-step process. First, DNS must be appropriately configured for each domain being served including an MX record, as documented in the BIND chapter of this book. Second, the new domain is added to the Local Domains table. Finally, one or more entries are added to the Address Mapping table. As DNS has its own chapter, and adding an entry to the Local Domains table was covered in the preceding tutorial, you’ll only learn the final step here.

# Adding Address Mapping Entries

Click on the Address Mapping icon, and create new mappings as appropriate for your environment. To create a new entry, select Address and fill in the address on which mail will be received in the Mail for field. This will include the name and domain name of the recipient, so for example, I might enter joe@virtualhost.com in this field. Next, select the Address option and enter the destination mailbox for this user in the, which needs to be an existing user, into the Send to field. For example, I might enter a username of virtualhost-joe here. The username must be created on the system, as well, which can be done using the section called "Users and Groups" in Chapter 5.

Click the Create button, and test your work by sending mail to your newly created virtual user.