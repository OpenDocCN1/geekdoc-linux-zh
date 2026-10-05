# Chapter 20

# Electronic Mail

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