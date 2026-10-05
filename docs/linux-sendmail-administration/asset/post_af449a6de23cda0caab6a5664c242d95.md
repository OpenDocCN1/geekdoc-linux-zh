
confXF_BUFFER_SIZE Defines the maximum amount of buffer memory that can be used for a transcript file before the file must be written to disk. The default is 4096 bytes. [ScriptFileBufferSize]

Despite the enormous length of this list, there are more define parameters. Additional lists of parameters are covered under the DOMAIN and the OSTYPE macros later in the appendix. define commands are the most common commands in the m4 source files. The next most commonly used is the FEATURE macro.

## FEATURE

The FEATURE macro processes m4 source code from the cf/feature directory. Source files in that directory define optional Sendmail features. The syntax of the FEATURE macro is:

```
FEATURE(name, argument])
```

The argument field is optional. If an argument is passed to the source file, the argument is used by the source file to generate code for the sendmail.cf file. For example:

```
FEATURE('mailertable', `dbm /etc/mail/mailertable')
```
generates the code for accessing the mailertable and defines that table as being a dbm database located in the file /etc/mail/mailertable.

The available features are listed in Table A.2. The table provides the name of each feature and its purpose.

## Table A.2 Features

| Name | Purpose |
|---|---|
| accept_unqualified_senders | Allow network mail from addresses that do not include a valid hostname. |
| accept_unresolvable_domains | Accept mail from hosts that are unknown to DNS. |
| access_db | Use the access database to control relaying. |
| allmasquerade | Masquerade recipient addresses. |

## Table A.2 Features (continued)

| Name | Purpose |
| --- | --- |
| always_add_domain | Add the local hostname to all locally delivered mail. |
| bestmx_is_local | Accept as local, mail addressed to a host that lists us as MX server. |
| bitdomain | Use a table to map BITNET hosts to Internet addresses. |
| blacklist_recipients | Filter incoming mail based on values in the access database. |
| delay_checks | Delay the check_mail and check_relay rules until check_rcpt is called. |
| dnsbl | Reject mail from hosts listed in a DNS-rejected list. Replaces rbl. |
| domaintable | Map domain names using a domain table. |
| generics_entire_domain | Map domain names identified in class G through the genericstable. |
| genericstable | Use a table to rewrite local addresses and addresses from class G. |
| ldap_routing | Enable LDAP-based email routing. |
| limited_masquerade | Only masquerade hosts listed in =M. |
| local_lmtp | Use mail.local with LMTP support. |
| local_procmail | Use procmail as the local mailer. |
| loose_relay_check | Disable validity checks for addresses that use the % hack. |
| mailertable | Route mail using a mailer table. |

## Appendix A m4 Macro Command Reference

**Table A.2** Features (continued)

| Name | Purpose |
| --- | --- |
| masquerade_entire_domain | Masquerade all hosts within the masquerading domains. |
| masquerade_envelope | Masquerade the envelope sender address in addition to the header sender address. |
| no_default_msa | Allow the default configuration of the Message Submission Agent to be overridden by the DAEMON_OPTIONS macro. |
| nocanonify | Don't convert addresses and hostnames using DNS. |
| nodns | Don't include DNS support. |
| nouucp | Don't include UUCP address processing. |
| nullclient | Forward all mail to a central server. |
| promiscuous_relay | Relay mail from any site to any site. |
| rbl | The obsolete Realtime Blackhole List feature has been replaced by dnsbl. |
| redirect | Support the .REDIRECT pseudo-domain. |
| relay_based_on_MX | Relay mail for any whose MX record points to this server. |
| relay_entire_domain | Relay mail for any host in your domain. |
| relay_hosts_only | Only relay mail for hosts listed in the access database. |
| relay_local_from | Relay mail if the source is a local host. |
| relay_mail_from | Relay mail if the sender is listed as RELAY in the access database. |
| smrsh | Use smrsh as the pro maililer. |

## Table A.2 Features (continued)

| Name | Purpose |
|--- |--- |
| stickyhost | Treat “user” differently than “user@local.host.”. |
| use_ct_file | Load $=t from the file defined by confCT_FILE. |
| use_cw_file | Load $=w from the file defined by confCW_FILE. |
| uucpdomain | Use a table to map UUCP hosts to Internet addresses. |
| virtuer_entire_domain | Map entire domain names through the virtuertable. |
| virtuertable | Map virtual domain names to real mail addresses. |

FEATURE macros remove unused lines from the sendmail.cf file. noucp removes the code to handle UUCP addresses for systems that do not have access to UUCP networks, and nodrs removes the code for DNS lookup for systems that do not have access to DNS. nullican disables the code that converts nicknames and IP addresses into hostname. Finally, the nullClient strips the code that converts nicknames and IP addresses into hostname.

Many features relate to relaying and masquerading. These are: stickyhost, allmasquerade, relay_based_on_MX, relay_hosts_only, and masquerade_entire_domain.

Several features define databases that are used for special processing. These are: domaintable, bitdomain, uucpdomain, and genericstable.

The genericstable is often used to convert the same addresses as those processed for masquerading, so the features affect masquerading and the genericable are set in the same way. If you use the genericstable and you use masquerading, set GENERIC_DOMAIN and GENERIC_DOMAIN_FILE to set the values you set for MASQUERADE_DOMAIN and MASQUERADE_DOMAIN_FILE.
