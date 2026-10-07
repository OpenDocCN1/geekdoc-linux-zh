# The feature Directory

The feature directory contains the m4 source code files that implement various Sendmail features. 4.6 shows that there are more than 40 features available.

# Listing 4.6 The feature Directory

```
[craig]$ ls m4
accept_unqualified_senders.m4
accept_unresolvable_domains.m4
access_db.m4
allmasquerade.m4
always_add_domain.m4
bestmx_is_local.m4
bitdomain.m4
blacklist_recipients.m4
delay_checks.m4
dnsbl.m4
domaintable.m4
generics_entire_domain.m4
genericstable.m4
ldap_routing.m4
limited_masquerade.m4
local_lmtp.m4
local_procmail.m4
loose_relay_check.m4
mailertable.m4
masquerade_entire_domain.m4
masquerade_envelope.m4
no_default_msa.m4
nocanify.m4
odns.m4
notsticky.m4
nouucp.m4
nullclient.m4
promiscuous_relay.m4
rbl.m4
redirect.m4
relay_based_on_MX.m4
relay_entire_domain.m4
relay_hosts_only.m4
relay_local_from.m4
relay_mail_from.m4
smrsh.m4
stickyhost.m4
use_ct_file.m4
use_cw_file.m4
uucpdomain.m4
virtuer_entire_domain.m4
virtuasable.m4
```

Describing these features and how they are used is one of the major tasks of this book.

# The m4 Directory

The last subsubdirectory in the cf directory is the m4 directory. This is the directory that contains the m4 macro definitions and the sendmail.cf skeleton code to build a sendmail.cf configuration file. Remember that m4 is not a language designed to build Sendmail configurations. It is a general-purpose macro language. The commands you use to build a Sendmail configuration are macros defined by the Sendmail developers. This is the directory that contains the definitions of these macro commands. The cf/m4 directory contains only four files.

```
[craig]$ ls m4
cf.m4 cfhead.m4 proto.m4 version.m4
```