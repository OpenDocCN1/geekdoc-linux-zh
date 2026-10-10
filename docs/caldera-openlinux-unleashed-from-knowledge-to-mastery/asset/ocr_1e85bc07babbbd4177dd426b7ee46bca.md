+   - Create a DNS MX record for each client machine, redirecting to the hub all mail addressed to the client.
+   - Change the Sendmail configuration on the hub so that mail addressed to client machines will be deliverable on the hub.

# Client Configuration

To configure a client machine on a network using a mail hub, you must do two basic things: (1) configure delivery agents to direct mail to hub and (2) configure rewrites to rewrite sender address to appear to be from the hub. This is accomplished by making a special client sendmail.cf. How this is done will vary between versions of sendmail. Generating this file by hand can be complex. However, it is also possible to generate this file using m4, as outlined in the section on configuring Sendmail.

Here is the m4 code that would be used to generate a client sendmail.cf:

```
include(`../m4/cf.m4')
VERSIONID(`linux for smtp-only setup')dnl
OSTYPE(Linux)
MASQUERADE_AS(thenetetfect.com)
define(`STATUS_FILE','`/var/log/sendmail.st')
define(`HELP_FILE','`/usr/share/sendmail/sendmail.hf')
FEATURE(always_add_domain)
EXPOSE_USER(root)
EXPOSE_USER(postmaster)
EXPOSE_USER(MAILER_DAEMON)
FEATURE(nulliclient,`mail.thenetetfect.com')
```

Here, mail.thenetetfect.com would be replaced with the name of the mail hub.

Do the following to generate this file using COAS:

+   1. Select COAS:Network:Mail Transfer.
+   2. In the Visible Domain dialog box, enter the domain you are in (for example, thenetetfect.com).
+   3. In the Mail Relay Host dialog box, enter the name of your mail hub (for example, mail.thenetetfect.com).
+   4. Leave the Transport Method drop-down dialog box set to SMTP.
+   5. Check the Relay Is Internet Hub check box. (In point of fact, you could leave this option unchecked and only check the Relay Is Local Hub option. Either way will produce the same sendmail.cf file. Checking both options clearly establishes what you are doing given that the hub will be both a local and an Internet relay.)
+   6. Check the Relay Is Local Hub check box.
+   7. Click OK to confirm your decision.