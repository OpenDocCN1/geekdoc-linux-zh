Here are some key points to note about the /etc/mail/sendmail.mc file:

![](bbox=[0.15, 0.22, 0.24, 0.3])

+   - `VERSIONID(`'setup for Red Linux'`) macro inserts the version information enclosed in quotes into the output.
+   - `OSTYPE(`'linux'`) specifies Linux as the operating system. You have to specify this macro early to ensure proper configuration. Placing this macro right after the `VERSIONID` macro is customary.
+   - `MAILER(smtp)` describes the mailer. According to instructions in the `/usr/share/sendmail-cf/README` file, `MAILER` declarations are always placed at the end of the `sendmail.mc` file, and `MAILER(smtp)` always precedes `MAILER(procmail)`. The mailer `smtp` refers to the SMTP mailer.

+   - `FEATURE` macros request various special features. For example, `FEATURE(`'blacklist_recipients'`)` turns on the capability to block incoming mail for certain usernames, hosts, or addresses. The specification for what mail to allow or refuse is placed in the access database (`/etc/mail/access.db` file). You also need the `FEATURE(`'access_db'`)` macro to turn on the access database.
+   - `MASQUERADE_AS(`'mydomain.com'`)` causes `sendmail` to label outgoing mail as having come from the host `mydomain.com` (replace with your domain name). The idea is for a large organization to set up a single `sendmail` server that handles the mail for many subdomains and makes everything appear to come from a single domain (for example, mail from many departments in a University appear to come from the University’s main domain name).
+   - `MASQUERADE_DOMAIN(subdomain.mydomain.com)` instructs `sendmail` to send mail from an address such as `user@subdomain.mydomain.com` as having originated from the same username at the domain specified by the `MASQUERADE_AS` macro.

The `sendmail` macros such as `FEATURE` and `MAILER` are described in the `/usr/share/sendmail-cf/README` file. Consult that file to find out more about the `sendmail` macros before you make changes to the `sendmail.mc` file.

![](bbox=[0.15, 0.76, 0.24, 0.84])

Typically, you have to add your system’s host name in the last line of the `/etc/mail/sendmail.mc` file. Follow these steps to add the host name:

+   1. If the host name is mycompany.com, edit the Cw line in /etc/mail/sendmail.mc as follows:
+   `Cwlocalhost.localdomain mycompany.com mycompany`