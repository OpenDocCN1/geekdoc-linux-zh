To illustrate how we test the left-hand-side and assign values to the right-hand-side, consider the following example.

```
R$<s*$>*$      $2      basic RFC822 parsing
```

If you apply the following input address to the rule:

```
Full Name <user@some.domain>
```

On the LHS, the first $* matches the string Full Name and this value is assigned to $1, < matches the literal < in the address, the second $* matches user@some.domain, and is assigned to the variable $2. The literal > matches > in the address. The third $* matches a null value.

The RHS is assigned the value $2 which resolves to user@some.domain.

The third field is a comment.

# THE SEMANTICS OF RULE SETS

A rule set is a group of rules that can be referenced as a set, and the set is given a number. The $<n> command marks the beginning of a rule set, where n is the number that references the rule set.

Rule sets are like subroutines or functions that process email addresses. They are called from individual rules, mailer definitions, and directly by sendmail itself. Six rule sets have special functions and are called directly by sendmail:

+   - Rule set 3 is applied first to all addresses. It converts an address to the canonical form: `local.part@host.domain`. If the address contains no @ sign then the host.domain part may be appended by sendmail. This happens only if the mail is received from a mailer that sets the C flag. SMTP mailers set this flag.

+   - Rule set 0 is applied after rule set 3 only to the recipient addresses actually used for mail delivery. It resolves the address to the mailer, host, and user triple. The triple is composed of the name of the mailer, the recipient’s hostname, and the recipient’s username.

+   - Rule set 1 is applied to all sender addresses in the message. It is usually not used. A standard `sendmail.cf` file will not have a definition for rule set 1. A custom rule set 1 is written at some sites to make all outgoing mail to appear to come from a central mail server.

+   - Rule set 2 is applied to all recipient addresses in the message. Like rule set 1, rule set 2 is also generally not used. Rule set 2 is sometimes used for debugging purposes.

+   - Rule set 4 is applied to all addresses in the message and is used to translate internal address formats to external address formats. Just like rule set 3, which is applied first to all addresses, rule set 4 is applied last to all addresses. Its purpose is to undo any special processing done by rule set 3. It removes trailing dots from fully qualified domain names. If rule set 3 had converted the commas of source route addresses to colons, rule