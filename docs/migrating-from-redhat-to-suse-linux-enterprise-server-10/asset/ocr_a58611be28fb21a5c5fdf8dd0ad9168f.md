# **The sender_canonical Lookup Table**

You can use the /etc/postfix/sender_canonical lookup table to rewrite sender addresses of incoming and outgoing emails (for outgoing email: login@host_internal.com to firstname.surname@mycompany.com).

The cleanup daemon reads this table when an email arrives before the generic lookup table /etc/postfix/canonical is read.

The following topics are described:

+   - Activate the Lookup Table
+   - The sender_canonical Lookup Table Format

# **Activate the Lookup Table**

This function is activated in the file /etc/postfix/main.cf by the entry

```
```
sender_canonical_maps = hash:/etc/postfix/sender_canonical
```
```

# **The sender_canonical Lookup Table Format**

Each line defines a rule that is evaluated by smtpd when an email arrives.

The rules are processed from top to bottom and the matching of rules ends when the first match occurs.

Each line consists of the definition of an email address in the first column and a defined action in the second column.

Possible values for email address patterns are

+   - **user@domain**. Defines a filter for the specified email address.