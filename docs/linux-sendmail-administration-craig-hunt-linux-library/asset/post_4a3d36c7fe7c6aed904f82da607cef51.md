
# Chapter 5 Understanding a Vendor's Configuration

canonify input: craig
Canonify2 input: craig
Canonify2 returns: craig
canonify returns: craig
1 input: craig
1 returns: craig
HdrFromL input: craig
AddDomain input: craig
AddDomain returns: craig < @LOCAL*
MasqHdr input: craig < @ @LOCAL*
MasqHdr returns: craig < @wren.foobirds.org.
HdrFromL returns: craig < @wren.foobirds.org.
final input: craig < @wren.foobirds.org.
final returns: craig < @wren.foobirds.org
> ^D

We run two tests using Sendmail -bt mode. In both cases we use a header/address, and we give it the address craig to process through the local mailer. The first test uses the generic-linux.cf configuration, which does not use the always_add_domain feature. The address goes in as comes out craig. In the second test we use the redhat.cf configuration, which uses the always_add_domain feature. In this test, craig is converted to craig@wren.foobirds.org. The effect of always_add_domain is clearly shown.

This is a good feature to use. The address shown, on local mail, is valid everywhere. This helps avoid confusion among your users, and confused users you want to avoid!

access_db This feature allows Sendmail to use the access database to decide what hosts, domains, and networks are acceptable sources of e-mail. An optional argument that defines the database type and path can be used with the access_db feature. The default database type is hash and the default path is /etc/mail/access. The access database is described in Chapter 6. In its fighting spam is covered in Chapter 11.

blacklist_recipients This feature allows the access database to be used to block mail from specific recipients. Normally, the access database is used to control mail from undesirable sources. With this feature, the access database also can be used to control mail bound for certain destinations. The blacklist_recipients feature is covered in detail in Chapter 11.

accept_unresolvable_domains This tells Sendmail to accept mail from a source if the domain name of the source cannot be resolved by DNS. By default, Sendmail takes the hostname in the MAIL FROM: header and asks DNS to map that name back to an address before it will accept incoming mail. This option overrides that default behavior.

Allowing mail from unsolvable domains is a potential security problem, but this feature is often necessary for systems that do not have full-time DNS service. Such systems are laptops that might be disconnected from the network or systems sitting behind a firewall that are not given full DNS access. The Red Hat configuration includes this feature because Red Hat must create a configuration that will work with the widest range of systems. If you have full-time DNS service for your network—and you should—remove this feature from your configuration.

Following this match of FEATURE commands are two MAILER commands. The first is the MAILER(smtp) command that we have already described. The second is the MAILER(procmail) command. Looking at it, you might think it has something to do with the local_procmail parameter described earlier. It doesn't. local_procmail means to do what the mailer named local will use the program procmail. MAILER(procmail) means that a mailer named procmail will use the procmail program will be added to the configuration. These two are unrelated. The mailer installed by MAILER(procmail) is used only if you configure entries in the mailtable to use it.

It's a big configuration that includes important capabilities, such as smsh, and not so important capabilities, like MAILER(procmail). As we saw in Chapter 4, this configuration works fine and delivers mail for our Red Hat system. But it is only a start. The discussion of the accept_unresolvable_domains feature and the comments inside the redhat.mc file make clear, we are expected to create our own configuration that suits us. In the next section we do just that. Starting with the redhat.mc file, we create our own Red Hat configuration.

# Modifying the Red Hat Configuration

There are lots of good things in the redhat.mc configuration, a couple of undesirable things, and a few redundancies. Since we are going to rewrite the configuration, I think we should also reorganize it to move some things out of the macro configuration file into macro source files where those items are a better fit. As a result, we will edit the redhat.mc file, create a new OTYPE type, and create a new DOMAIN file. To do this we first

![](img/9639113aa446fb8976cb3d377f7aafdd_154_0.png)

copy redhat.mc to redhat81.mc, octype/linux.m4 to octype/redhat7.0.m4, and domain/generic.m4 to domain/foobirds.m4.

Next we edit the files. First I edited the macro configuration file, redhat81.mc, changing the DOMAIN command to foobirds.m4 instead of generic.m4. Then I moved the CONF_USER_ID parameter to the new OYPE file because I consider the user ID and group ID setting specific to Red Hat Linux. I deleted the undef defines because they serve no purpose. I also deleted CONFAUTO_REBUILD which is a deprecated option.

I considered moving CONF_CONNECT to the OYPE file because it is designed to override the default TCP timeout settings by the Linux operating system. Instead, I decided to delete it because I have not any TCP timeout periods and did not anticipate any. Likewise I considered moving CONF_NULL_LIST to the DOMAIN file because it is clearly needed to govern how MX records are handled. But I decided to delete the option because it causes Sendmail to handle MX records in a non-standard way. Unless I break a standard to get things running, I don't want to.

I deleted the CONF_PROBE_INTERFACES option because I want Sendmail to include all of the server's interfaces as part of class. The CONF_PROBE_INTERFACES option is primarily useful on laptop systems where PCMCIA interfaces may be added or removed from a running system. Since I'm not running my server on a laptop, for the same reason, I deleted the accept_unresolvable_domains feature from the configuration, which is primarily used on laptops. I have good DNS service and therefore should not use that feature.

Some lines required no decision. PROCMAIL_MAILER_PATH and local_procmail are already in the OYPE file, and redirect are already in the DOMAIN file. However, the confMAX_LENGTH that came from the generic.m4 file seemed unnecessary, so I deleted it from the DOMAIN file. I also set PROC_MAILER_PATH unconditionally.

I moved ALIAS_FILE, STATUS_FILE, and smsh to the OYPE file because mailer options are usually stored there. I deleted the UUCP_MAIL_MAX setting because the configuration does not define any UUCP mailers. I moved USERDB_SPEC, always_add_domain, access_db, and blacklist_recipients to the new DOMAIN file because I decided to put all domain, masquerading, and anti-spam configuration in that file. The remaining configuration commands I left in the macro configuration file. Confused? Take a look at Table 5.2. It lists every line from the original redhat.mc configuration file and tells us what we did with it.

# Table 5.2 Rewriting the Red Hat Configuration

| Command | Disposition |
|---|---|
| OSTYPE | Kept in the macro configuration file. |
| confDEF_USER_ID | Moved to the OYPE file. |
| UUCP_RELAY | Deleted. |
| BITNET_RELAY | Deleted. |
| confAUTO_REBUILD | Deleted. |
| confTO_CONNECT | Deleted. |
| confTRY_NULL_MX_LIST | Deleted. |
| confDONT_PROBE_INTERFACES | Deleted. |
| PROCMAIL_MAILER_PATH | Located in the OYPE file. |
| ALIAS_FILE | Moved to the OYPE file. |
| STATUS_FILE | Moved to the OYPE file. |
| UUCP_MAIL_MAX | Deleted. |
| confUSERDB_SPEC | Moved to the DOMAIN file. |
| smrsh | Moved to the OYPE file. |
| mailertable | Kept in the macro configuration file. |
| virtputable | Kept in the macro configuration file. |
| redirect | Located in the DOMAIN file. |
| always_add_domain | Moved to the DOMAIN file. |
| use_cw_file | Located in the DOMAIN file. |
| local_procmail | Located in the OYPE file. |
| access_db | Moved to the DOMAIN file. |
