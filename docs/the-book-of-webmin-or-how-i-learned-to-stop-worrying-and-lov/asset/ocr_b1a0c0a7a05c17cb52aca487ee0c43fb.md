can manually edit or view your aliases file. Be careful, as the format and entries will not be checked by Webmin for correctness. If you make a mistake your Sendmail may complain loudly (in the logs) and stop working.

# Local Domains

This page configures the sendmail.cf file and allows you to choose what domains Sendmail will accept local mail delivery for. By default Sendmail only accepts delivery for the local host. In order to accept mail for a whole domain, or a number of domains, they must be listed here. Also, the domains must have a DNS MX record that points to the server where your Sendmail is running. Sendmail can handle mail for any number of domains; however, setting up virtual hosting with Sendmail is a little tricky. A good document that describes the technique can be found on the Virtual Hosting With Sendmail [http://www.sendmail.org/virtual-hosting.html] page. Virtual hosting is also discussed briefly in the tutorial section of this chapter.

> NOTE
> For virtual hosting in Sendmail, you will also need to perform some configuration in Address Mapping and possibly in Outgoing Addresses (generics).

# Domain Masquerading

The Domain Masquerading page provides access to the domain masquerading features of Sendmail. This allows you to make all outgoing messages appear to be from the same domain. When a domain masquerading rule is in place, Sendmail will replace the From address of all outgoing mail to appear to come from the domain to be masqueraded as. Also see the Local Domains page for more as well as a helpful link regarding virtual hosting in Sendmail.

# Trusted Users

Ordinarily, Sendmail will not allow a user to claim to be a different user. However, if listed here, users will be trusted to claim they are another user or from another domain. Care should be taken when using this option, as it is one of the safeguards against spoofed email addresses.

# Address Mapping

An Address mapping is similar to an alias, except they are able to handle domain information, as needed by virtual domains. To create an address mapping, all you must do is enter the address or domain to act upon. And a send to action to perform on each message as it is received by Sendmail. For example, if I host the domain penguinfeet.org on my swelltech.com server, then I must set up a method for mail sent to sysadmin@penguinfeet.org to make it into my mailbox at joe. So, I would create a map wherein the Mail for address is sysadmin@penguinfeet.org and the Send to address is joe.