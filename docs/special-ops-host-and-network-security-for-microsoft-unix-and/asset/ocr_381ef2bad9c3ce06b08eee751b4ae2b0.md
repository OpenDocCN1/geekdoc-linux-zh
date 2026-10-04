# Chapter 7 • Securing Exchange and Outlook Web Access

+   - Restrict who is allowed to send mail to any distribution list with more than 25 members; this will help prevent abuse of the e-mail system and reduce the likelihood that viruses can be sent to large numbers of users.

+   - Remove shared folder Everyone for all shared folders.

+   - Restrict the Everyone group's administrative permission to create top-public folders.

+   - Designate servers to perform specific roles, and don't allow servers to perform multiple roles (such as a Web server and OWA server.) This allows you to tighten security as much as possible for that specific server role.

+   - Never configure an SMTP server to open relay; there is no reason for you to have an open SMTP relay.

+   - Never configure administrative and operator accounts for mailboxes.

+   - Statically map the system attendant's NSPI/DSProxy TCP ports and the information store's TCP port to an organizational standard.

+   - Regularly purge or archive virtual server and message tracking logs. These logs should be protected so that only administrators can access them.

In addition to best practices for security, I have a series of practices that I recommend Exchange administrators follow in order to keep their Exchange organizations stable and operating. Although most of these practices are not necessarily security-related they are nonetheless important. I recommend these procedures be incorporated into daily operations:

+   - Perform daily backups and examine the event logs to confirm that the backup occurred.

+   - Scan the event logs daily for security- and operations-related events.

+   - Confirm that virus signatures are up to date. Note any recent virus activity.

+   - Check the available disk space on all disks.

+   - Look at the SMTP queues and MTA queues (if applicable) for unusual growth.

Finally, there are a couple of things that I recommend be incorporated into an ongoing effort to keep the end-user community educated, to ensure that users make good use of the messaging system, and to keep their own data secure:

![](bbox=[0.065, 0.947, 0.299, 0.977])