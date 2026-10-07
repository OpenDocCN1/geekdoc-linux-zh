# Basic Rulesets 223

+   - canonify has a subsection named Canonify2, also known as ruleset 96, which is used to obtain canonical hostnames from DNS.

+   - parse has two subsections named Parse0 and Parse1, and a subroutine named ParseLocal (ruleset 98) that it calls to handle local addresses.

+   - Mailterable MailerToTriple, which is also known as ruleset 95, to help convert mailterable entries to mail deliveries, and it uses CanonLocal to put local names from the mailterable into a standard format.

+   - ParseRecipient uses Addr to put addresses into the standard format, which Addr does by simply calling Parse0 and Canonify.

+   - The bulk of the work of check_relay, check_mail, and check_rcpt is handled by subsections named Basic_check_relay, Basic_check_mail, and Basic_check_rcpt. In turn, Basic_check_rcpt calls RelayAuth to check client authentication when required. SearchList is another routine called by check_mail and check_rcpt to process an internal syntax used by these anti-spam filters. Recall the (src) class mentioned in Chapter 7; SearchList is what is used.

+   - tls_client and tls_server call tls_connection to get the connection verified. tls uses turn max to determine the appropriate number of cipher bits used. Transport layer security is discussed in Chapter 12, "Sendmail Security.",

Rulesets with rulesets rulesets rulesets segment the complex task of processing e-mail. This makes the task of processing mail manageable in turn creates confusion for the system administrator trying to understand what these rulesets do. My advice is: "Don't worry about it." A general idea of what these rulesets do is all that is required for Sendmail mastery. You don't need to modify the rulesets of Sendmail, even to create an advanced custom configuration. Instead, Sendmail provides empty rulesets for your hooks:

+   - sender (ruleset 1) is available for custom processing of sender addresses. See the LOCAL_RULE discussion in Chapter 9.

+   - recipient (ruleset 2) is available for custom processing of recipient addresses. See the LOCAL_RULE discussion in Chapter 9.

+   - Local_localaddr is available for custom processing of local addresses before they are processed by localaddr (ruleset 5).

+   - Local_check_relay is available to customize anti-spam relaying rules. It is called before check_relay. See the discussion of anti-spam rules in Chapter 11, "Stopping Spam."