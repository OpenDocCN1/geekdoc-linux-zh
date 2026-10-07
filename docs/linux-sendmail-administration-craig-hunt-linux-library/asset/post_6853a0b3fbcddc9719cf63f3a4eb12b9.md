
# Table A.2 Features (continued)

| Name | Purpose |
| :--- | :--- |
| always_add_domain | Add the local hostname to all locally delivered mail. |
| bestmx_is_local | Accept as local, mail addressed to a host that lists us as its MX server. |
| bitdomain | Use a table to map BITNET hosts to Internet addresses. |
| blacklist_recipients | Filter incoming mail based on values in the access database. |
| delay_checks | Delay the check_mail and check_relay rules until check_rcpt is called. |
| dnsbl | Reject mail from hosts listed in a DNS-based rejection list. Replaces rbl. |
| domainantable | Map domain names using a domain table. |
| generics_entire_domain | Map domain names identified in class G through the genericstable. |
| genericstable | Use a table to rewrite local addresses and addresses from class G. |
| ldap_routing | Enable LDAP-based e-mail routing. |
| limited_masquerade | Only masquerade hosts listed in=$M. |
| local_lmtp | Use mail.local with LMTP support. |
| local_procmail | Use procmail as the local mailer. |
| loose_relay_check | Disable validity checks for addresses that use the % hack. |
| mailertable | Route mail using a mailer table. |
| masquerade_entire_domain | Masquerade all hosts within the masquerading domains. |
| masquerade_envelope | Masquerade the envelope sender address in addition to the header sender address. |
| no_default_msa | Allow the default configuration of the Message Submission Agent to be overridden by the DAEMON_OPTIONS macro. |
| nocanonify | Don't convert addresses and hostnames using DNS. |
| nodns | Don't include DNS support. |
| nouuccp | Don't include UUCP address processing. |
| nullclient | Forward all mail to a central server. |
| promiscuous_relay | Relay mail from any site to any site. |
| rbl | The obsolete Realtime Blackhole List feature has been replaced by dnsbl. |
| redirect | Support the .REDIRECT pseudo-domain. |
| relay_based_on_MX | Relay mail for any site whose MX record points to this server. |
| relay_entire_domain | Relay mail for any host in your domain. |
| relay_hosts_only | Only relay mail for hosts listed in the access database. |
| relay_local_from | Relay mail if the source is a local host. |
| relay_mail_from | Relay mail if the sender is listed as RELAY in the access database. |
| smrsh | Use smrsh as the prog mailer. |
| stickyhost | Treat "user" differently than "user@local.host." |
| use_ct_file | Load $=t from the file defined by confCT_FILE. |
| use_cw_file | Load $=w from the file defined by confCW_FILE. |
| uucpdomain | Use a table to map UUCP hosts to Internet addresses. |
| virtuer_entire_domain | Map entire domain names through the virtertable. |
| virtertable | Map virtual domain names to real mail addresses. |

Several FEATURE macros remove unwanted lines from the sendmail.cf file. noucp removes the code to handle UUCP addresses for systems that do not have access to UUCP networks, and nodns removes the code for DNS lookups for systems that do not have access to DNS. nocanify disables the code that converts nicknames and IP addresses into hostnames. Finally, the nullclient strips everything out of the configuration except for the ability to forward mail to a single mail server via a local SMTP link. The name of that mail server is provided as the argument on the nullclient command—e.g., FEATURE(nullclient, big.isp.net) forwards all mail to big.isp.net without any local mail processing.

Many features relate to relaying and masquerading. Examples are: stickyhost, allmasquerade, relay_based_on_MX, relay_hosts_only, and masquerade_domain. All of these features, and all of the others relating to relaying and masquerading, are covered in the “DOMAIN” section of this appendix.

Several features databases are used to perform special address processing. All of these features accept an optional argument that defines the database. (See the sample mailertable command at the beginning of this section for an example of defining the database with the optional argument.) If the optional argument is not provided, the database description always defaults to hash -o /etc/mail/filename, where filename matches the name of the feature. For example, mailertable defaults to the definition hash -o /etc/mail/mailertable. The database features are:

- mailertable This database maps host and domain names to specific mailer:table pairs. The mailer, host, user triple is returned by rules 0 on the delivery address. The mailertable allows you to define the mailer and the host of the delivery pair based on the name in the delivery address.

If the host or domain name in the delivery addresses matches a key, the format is:
```
mailer:host
```
where the mailer and host are specified in the database. The database features are:

- mailertable This database maps host and domain names to specific mailer:table pairs. The mailer, host, user triple is returned by rules 0 on the delivery address. The mailertable allows you to define the mailer and the host of the delivery pair based on the name in the delivery address.

- mailertable This database maps host and domain names to specific mailer:table pairs. The key is the value returned.

- mailertable This database maps host and domain names to specific mailer:table pairs. The key is the value returned.

# Appendix A m4 Macro Command Reference
