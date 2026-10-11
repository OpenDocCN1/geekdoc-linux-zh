# **Activate the Lookup Table**

This function is activated in the file `/etc/postfix/main.cf` by the entry

```
```text
recipient_canonical_maps = hash:/etc/postfix/recipient_canonical
```
```

# **The recipient_canonical Lookup Table Format**

Each line defines a rule that is evaluated by smtppd when an email arrives.

The rules are processed from top to bottom and the matching of rules ends when the first match occurs.

Each line consists of the definition of an email address in the first column and a defined action in the second column.

Possible values for email address patterns are

+   - **`user@domain`**. Defines a filter for the specified email address.
+   - **`user`**. Defines a filter for all email addresses with the same user part, provided the domain part of the email is listed in one of the variables `$myorigin`, `$mydestination`, `$inet_interfaces`, or `$proxy_interfaces` of the file `/etc/postfix/main.cf`.
+   - **`@domain`**. Defines a filter for all email addresses of the specified domain.

Possible values for actions are

+   - **`user@domain`**. Rewrites the email addresses to the value defined here.

Examples:

```
```text
geeko@digitalairlines.com    training@digitalairlines.com
@s1c.digitalairlines.com    s1c@digitalairlines.com
```
```