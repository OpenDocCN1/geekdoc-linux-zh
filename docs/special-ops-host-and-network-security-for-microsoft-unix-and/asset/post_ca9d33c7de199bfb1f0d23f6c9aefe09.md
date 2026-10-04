
## Chapter 7 • Securing Exchange and Outlook Web Access

- Restrict who is allowed to send mail to any distribution list with more than 25 members; this will help prevent abuse of the e-mail system and reduce the likelihood that viruses can be sent to large numbers of users.

- Remove shared folder "Everyone" for all shared folders.

- Restrict the "Everyone" group's administrative permission to create top-public folders.

- Designate servers to perform specific roles, and don't allow servers to perform multiple roles (such as a Web server and OWA server.) This allows you to tighten security as much as possible for that specific server role.

- Never configure an SMTP server to open relay; there is no reason for you to have an open SMTP relay.

- Never configure administrative and operator accounts for mailboxes.

- Statically map the system attendant's NSPI/DSProxy TCP ports and the information store's TCP port to an organizational standard.

- Regularly purge or archive virtual server and message tracking logs. These logs should be protected so that only administrators can access them.

In addition to best practices for security, I have a series of practices that I recommend Exchange administrators follow in order to keep their Exchange organizations stable and operating. Although most of these practices are not necessarily security-related they are nonetheless important. I recommend these procedures be incorporated into daily operations:

- Perform daily backups and examine the event logs to confirm that the backup occurred.

- Scan the event logs daily for security- and operations-related events.

- Confirm that virus signatures are up to date. Note any recent virus activity.

- Check the available disk space on all disks.

- Look at the SMTP queues and MTA queues (if applicable) for unusual growth.

Finally, there are a couple of things that I recommend be incorporated into an ongoing effort to keep the end-user community educated, to ensure that users make good use of the messaging system, and to keep their own data secure:

![](img/729efc56f204a2ebffb8295c3a2dfdfb_404_0.png)

- Users should be taught to treat e-mail data as they would any other confidential or proprietary information.
- OWA users must close the Web browser window to terminate the HTTP session with the OWA server.
- Users should be reminded not to use their company/organization e-mail address on Web sites when registering for contests, doing online banking, requesting information, etc. This will help keep down the amount of spam they receive.
- The organization should develop an acceptable policy covering the usage of the e-mail system. This policy should define things that the end user should and should not do with the e-mail system. This can include sending out, objectionable jokes, garage sale notices, or large files.

## Security Checklist

I have broken down a couple of basic checklists to follow when securing Exchange 2000. Most of the items on these checklists are for all servers regardless of how secure you want to be. However, the last checklist is for those of us that are a little more paranoid. I'll let you decide how paranoid you need to be.

## Before Starting Exchange Review

Our first checklist takes us to the operating system and IIS level. Before we even consider securing Exchange 2000, the underlying OS must be secured.

- Confirm the OS is patched to the latest possible level (http://windowsupdate.microsoft.com).
- Disable unnecessary W2k Services (see Chapter 5).
- Remove the IISample, IISHelp, IISAdmin, MSADC, Printers, and Scripts IIS virtual directories, or let IIS Lockdown handle for you. (see Chapter 10).
- Confirm that local usernames have strong passwords and that the guest account is disabled (member servers). The local administrator and guest preferably should be renamed.

![](img/729efc56f204a2ebffb8295c3a2dfdfb_405_0.png)

- Disable NetBIOS on all network adapters unless the E2K server is providing file and print services to older clients. Unless you have only a single server in your organization, clients should never use the Exchange 2000 server for file and print services.
- Enable auditing (local logons, security policy changes).
- Organize Exchange 2000 servers into their own OU.

## Standard Exchange

Now that the platform is secure, let's move on to Exchange. One of the things I'm going to ask is to disable unnecessary services. This checklist should be completed before putting Exchange into production.

- Deploy anti-spam measures.
- Implement content inspection to look for unauthorized content, naughty words, etc.
- Implement anti-spam measures.
- Deploy anti-spam measures.
- Implement content inspection to look for unauthorized content, naughty words, etc.

- Disable unnecessary services (POP3, IMAP4, NNTP, Search, MTA).
- Confirm that no user or group has been given Receive permissions.

- Implement physical access controls.
- Deploy anti-spam measures.
- Deploy anti-spam measures.
- Implement content inspection to look for unauthorized content, naughty words, etc.

- Disable unnecessary services (POP3, IMAP4, NNTP, Search, MTA).

- Confirm that no user or group has been given Receive permissions.

## High Exchange 2000

- Implement a data center firewall between users and all servers on the organization backbone.
- Configure E2K to accept only specific MAPI client versions.
- Configure storage groups to zero out deleted database pages.

Now that the platform is secure, let's move on to Exchange. One of the things I'm going to ask is to disable unnecessary services. This checklist should be completed before putting Exchange into production.

- Deploy anti-spam measures.
- Implement content inspection to look for unauthorized content, naughty words, etc.

- Disable unnecessary services (POP3, IMAP4, NNTP, Search, MTA).

- Confirm that no user or group has been given Receive permissions.

## Front-End/Back-End Server Considerations

Here are a few considerations for servers that are running in front-end/back-end configuration:

- Disable unnecessary services (POP3, IMAP4, NNTP, Search, MTA).
- Enable/require SSL for HTTP, POP3, IMAP4, and NNTP clients.

## High Security 2000

If you have decided to go for “extreme” security, you have come to the right checklist. Each of these is requiring a bit more work on your part, especially if you decide to distribute certificates:

- Put Exchange 2000 servers on switched segments.
- Implement IPSec between all Exchange 2000 servers and to/from Windows 2000 domain controllers.
- Distribute X.509v3 certificates to all users to allow use of message signing and encryption

## Alternative Controls

I have almost ignored the subject of content inspection and anti-spam systems, mainly because anti-spam systems and content inspection systems increase the amount of administrative overhead by quite a bit. This is because anything that falls under the scrutiny of these systems usually has to be inspected manually by an administrator. I know a number companies that successfully use content inspections systems as Mail Sweeper, but be aware, these systems such as Mail Sweeper, will increase your overall overhead.

- Implement content inspection to look for unauthorized content, naughty words, etc.
- Deploy anti-spam measures.
