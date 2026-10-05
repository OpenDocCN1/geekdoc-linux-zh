# Exercises

The Exim specification is the defining document for Exim configuration. It is very complete and is updated with each new distribution. A text version is included in the file doc/spec.txt in the distribution, and a PDF version is available from exim.org. There are several how-to documents on the web site.

# Postfix references

BLUM, RICHARD. Postfix. Sams Publishing, 2001.

DENT, KYLE D. Postfix: The Definitive Guide. Sebastopol, CA: O'Reilly Media, 2003.

HILDEBRANDT, RALF, AND PATRICK KOETTER. The Book of Postfix: State of the Message Transport. San Francisco, CA: No Starch Press, 2005.

This book is best; it guides you through all the details of Postfix configuration, for complex environments. The authors are active in the Postfix community and participate regularly on the postfix-users mailing list. The book is unfortunately out of print, but used copies are easily available.

postfix.org/SOHO_README.html is a guide to using Postfix at home or in a small office environment.

# RFCs

RFCs 5321 and 5322 are the current versions of RFCs 821 and 822. They define the SMTP protocol and the formats of messages and addresses for Internet mail. RFCs 5335 and 5336 cover extensions for internationalized email addresses. There are currently almost 90 email-related RFCs, too many to list here. See the general RFC search engine at rfc-editor.org for more.

# 20.19 Exercises

+   E20.1 Briefly explain the difference between a user agent (MUA), and an access agent (AA). Then explain the difference between a mail transport agent (MTA) and a mail submission agent (MSA).
E20.2 Inspect the mail queue on your local mail server. Are there messages with no control files or control files with no messages? What is the oldest message in the queue? (Requires root access)
E20.3 Explain what an MX record is. Why are MX records important for mail delivery? Give an example in which a misconfigured MX record might make mail undeliverable.
E20.4 Determine the design of mail service at your site and diagram in the style of Exhibit B on page 754. Where is incoming mail scanned for spam or viruses? What about outgoing mail?

![](bbox=[0.943, 0.222, 0.985, 0.358])