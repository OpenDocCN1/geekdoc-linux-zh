# Activate the Lookup Table

This function is activated in the file /etc/postfix/main.cf by the entry

```
alias_maps = hash:/etc/aliases
```

# The aliases Lookup Table Format

Each line defines a rule that is evaluated by smt pd when an email arrives.

The rules are processed from top to bottom and the matching of rules ends when the first match occurs.

Each line contains

+   - First column: A local recipient address followed by a colon.
+   - Second column: Filtered email is then redirected to another email user or to another email alias.
+     - Details of the target recipient in the second column can also be extended to include multiple recipients using a comma-separated list.
+     - An email is delivered explicitly to a local user if the recipient address in the second column begins with a `\`.
+     - The following is an example:.

```
```
root: 		\root, geeko
mailer-daemon:	root
postmaster:	mailer-daemon
daemon:		root
webmaster:		tux@digitalairlines.com
wwwrun:		webmaster
```
```

1 HARDCOPY PERMITTED-NO DISTRIBUTION ALLOWED