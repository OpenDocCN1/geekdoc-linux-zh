
## Chapter 20 Electronic Mail

Using the colon as a value separator presents a problem when you express IPv6 addresses, which use colons as parts of the address. You can escape the colons by doubling them, but the easiest and most readable fix is to redefine the separator character with the < character as assign values to the option. For example, both of the two lines set the value of the localhost_interfaces option, which contains the IPv4 and IPv6 localhost addresses:

```
local_interfaces = 127.0.0.1 ::1
local_interfaces = <; 127.0.0.1 ::1
```

The second form, in which the semicolon has been defined as the separator, is more readable and less fragile.

There are a options—more than 500 in the options index of the documentation. And we said sendmail was complicated! Most options have sensible defaults, and all have descriptive names. It's handy to have a copy of the doc/spec.txt file from the distribution in your favorite text editor when you are researching a new option. We don't cover all the options, just the ones that occur in our example configuration.

## Lists

Exim has four kinds of lists, introduced by the keywords hostlist, domainlist, addresslist, and localpartslist. Here are two examples using hostlist:

- + hostlist_my_relay_list = 192.168.1.0/24 : friend.example.com
- hostlist_my_relay_list = /usr/local/exim/relay_hosts.txt

Members can be listed in-line or taken from a file. If in-line, they are separated by colons. There can be up to 16 named lists of each type. In the in-line example above, we include all machines on a local /24 network and a specific hostname.

The symbol @ can be a member of a list; it means the name of the local host and makes it possible to write a single generic configuration file for most nonhosts at your site. The notation [] is also useful and means all IP addresses on which Exim is listening; that is, all IP addresses of localhost.

To reference a list, just put + in front of its name to match the list or ! to match nonmembers; for example, +my_relay_list. There must be no space between + and the name of the list.

Lists can include references to other lists and the $ indication name. Lists that include references to variables (e.g., $variable_name) make processing slower because Ultim cannot cache the results of evaluating the list, which it does by default.

## Macros

You can use macros to define parameters, error messages, etc. The parsing is primitive, so you cannot define a macro whose name is a subset of another macro unpredictable.

## ACLs (access control lists)

The syntax is

```
MACRO_NAME = rest of the line
```

For example, the first of the following lines define a macro named ALIAS_QUERY that looks up a user's alias entry in a MySQL database. The second line shows the use of the macro to do an actual lookup, with the result being stored in the variable called data.

```
ALIAS_QUERY = \
select mailbox from user where login = '${quote_mysql:$local_part}';
data = [$lookup mysql[ALIAS_QUERY]]
```

Macro names are not required to be all caps, but they must begin with a capital letter. However, the all-caps convention adds clarity. The configuration file can include ifdefs evaluate a macro and use it to determine whether or not to include a portion of the config file. Every imaginable form of ifdef is supported, all begin with a dot.

## ACLs (access control lists)

Access control lists filter the addresses of incoming messages and either accept or deny. They divides addresses into a local part that represents the user and a domain that is the recipient's domain.

ACLs can be applied at any of the various stages of an SMTP conversation: HELO, MAIL, RCPT, DATA. Typically, an ACL enforces strict adherence to the SMTP protocol at the HELO stage, checks the sender and the sender's domain at the MAIL stage, checks the recipients at the RCPT stage, and scans the message content at the DATA stage.

A few options means acl_smtp_command specify which ACL should be after each command in the SMTP protocol. For example, the acl_smtp_rcpt option specifies the ACL to run on each address that is a recipient of the message. You can define ACLs in the acl section of the config file, in a line that referenced by the acl_smtp_command, or in-line when the option is defined.

A sample called my_check_rcpt is defined below. We would invoke it by assigning its name to the acl_smtp_rcpt option in the global options of the config file. If this ACL denies an address at the RCPT command, the sending server should give up and not try the address again. Another ACL to use is acl_smtp_data, which would run on the message after it has been received, for example, to count scan.

```
begin acl
  my_check_rcpt:
    accept
      control = dkim_disable_verify
    deny
      message = Restricted characters in address
      domains = +local_domains
      local_parts = ^[\@:] : ^*@%!/]
```

![](img/579efec8c67772f31ecf34844bbb71a2_863_0.png)

## Chapter 20

## Electronic Mail

deny message = Restricted characters in address
domains = !+local_domains
local_parts = ^[^/] : ^*\@%!] : ^*\\\\\

accept local_parts = postmaster
domains = +local_domains

require verify = sender
accept hosts = +relay_from_hosts
control = submission
control = dkim_disable_verify

accept authenticated = *
control = submission
control = dkim_disable_verify

require message = Relay not permitted
domains = +local_domains : +relay_to_domains
require verify = recipient
accept

This ACL, adapted from examples in the Exam documentation, ends with a default-fault accept; you might want to rethink your ACLs to deny by default, as firewalls typically do. The default name for this access control list is acl_check_report; you should probably not change its name (as we did, to emphasize that the name is something you specify, not a predefined Exam configuration option).

The first accept line, containing a comma, is an empty list. of remote hosts matches cases in a local MUA submitted a message on the MTA's standard input. If the address being tested meets this condition, the ACL accepts the addresses and DKIM signature validation, which is turned on by default. If the address does not match this address clause, control drops through to the next clause in the ACL definition.

The first deny stands intended for messages coming into your local domains. It rejects any address whose local part (the username) starts with a dot or contains the special characters @, %, |, or |. The second deny applies to messages sent out by your users. It, too, disallows special characters and sequences in the local parts of addresses, in case your users' machines have been infected with a virus or other malware. In fact, such addresses have been used by spammers to confuse ACLs or of creating security problems.

In general, if you are intending to use $local_parts (supposed, the recipient's username) in a directory path (to store mail or look for a vacation file, example) please be very careful that your ACLs have filtered out any special characters that could cause unwanted behavior. (This example looks for the sequence ../, which could be problematic if the username is inserted into a path.)

## ACLs (access control lists) 817

The next accept stanza guarantees mail to postmaster will always get through if it's sent to a local domain; this can help with debugging.

The require line checks if a bounce message can be returned, but it checks only the sender's domain. If the sender's username is forged, a bounce could still fail.

The next accept stanza checks for hosts that are allowed to relay through, namely local hosts that submitting mail into the system. The control line specifies that exist as a mail agent and fix any header deficiencies as the message arrives. DKIM verification is disabled because these messages are outbound from your users.

The last accept stanza deals with local hosts that authenticate via SMTP AUTH. Once again, these messages are treated as transmissions from user agents.

We next check the domain to which the message is headed and whether it is in our list of local_domains or in our list of domains to which we allow relay, relay_to_domains. Any destinations not in one of those lists are refused with the specified error message. DKIM verification is again disabled.

Finally, when all previous requirements have been met but no-specific accept or deny has been triggered, we verify the recipient and accept the message. Internet messages to local users fall into this category.

We haven't included any blacklist scanning in the example above. To access a blacklist, use one of the examples in the default config file or something like this:

```
deny condition = {$if ip4($sender_host_address)}
authenticated = *
hosts = +my_whitelist_ips
dnslist = list.dnswl.org
domains = +local_domains
verify = recipient
message = You are on R $dnslist_domain: $dnslist_text
dnslist = zen.spamhaus.org
logwrite = Blacklisted sender {$sender_host_address} \
$dnslist_domain: $dnslist_text
```

Translated to English, this code specifies that if a message matches all of the following criteria, it is rejected with a custom error message and logged (also with a custom message).

+   1. require means "deny if not matched."
