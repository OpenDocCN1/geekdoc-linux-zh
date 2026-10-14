domains that are hosted by Postfix. So, by default, Postfix is not an open relay. This is a good beginning and may be all that is needed in many environments. However, because UCE is such a nuisance for users and network administrators, it may be worthwhile to implement more advanced filtering. This section will address the basics of the Postfix UCE control features.

# Access Control List Order

Every message that enters the smtpd delivery daemon will be processed by a number of access control lists and checked against a number of rules to ensure that the message is one that the administrator actually wants delivered. The goal for most administrators is to prevent unsolicited commercial email from passing through these rules, yet allow every legitimate email to be delivered. This is a lofty goal and a delicate balance. No perfect solution exists, as long as people are willing to steal the resources of others for their own commercial gain and go to great lengths to overcome the protections in place to prevent such abuse. However, in most environments it is possible to develop a reasonable set of rules that prevents most spam and allows most or all legitimate mail through unharmed.

It is important to understand the order of processing if complex sets or rules are to be used, as attempting to use a particular rule too early in the chain can lead to subtle errors or strange mail client behavior. Because not all clients react exactly correctly to some types of refusals, and not all clients create correctly formed SMTP requests, it is not unlikely that a misplaced rule will lock out some or all of your clients from sending legitimate mail. It could also just as easily lead to opening a hole in your spam protections early in the rule set, which would allow illicit mail to pass.

The Postfix UCE controls begin with a couple of simple yes or no checks, called smtpd_helo_required and strict_rfc821_envelopes, both configured in the SMTP Server Options page. The first, if enabled, requires a connecting mail client to introduce itself fully by sending a HELO command. This can stop some poorly designed bulk email programs. The second option requires for the envelope to fit the SMTP specification precisely, thus enforcing complete headers. Though the envelope and HELO can be forged by a bulk mailer, it may stop the more hastily implemented variants (well, how many good programmers do you know that write tools to help spammers?).

The next stage is the four SMTP restrictions also found on the SMTP Server Options page. These further limit from where and to where mail will be delivered. The order of traversal for these four lists of rules is:

+   1. **Restrictions on client hostnames/addresses** or `smtpd_client_restrictions`
+   2. **Restrictions on sends in HELO commands** or `smtpd_helo_restrictions`
+   3. **Restrictions on sender addresses** or `smtpd_sender_restrictions`
+   4. **Restrictions on recipient addresses** or `smtpd_recipient_restrictions`

Each of these checks can return REJECT, OK, or DUNNO. If REJECT, the message will be refused, and no further rules will be checked. If OK, no further rules in the given restriction will be checked, and the next restriction list will be checked. If