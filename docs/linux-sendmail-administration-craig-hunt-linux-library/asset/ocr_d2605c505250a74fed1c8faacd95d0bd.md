# Mailer Triple Variations

There are a few variations on the mailer triple syntax that are also used in the templates of some rules. Two of these variations use only the “mailer” component.

$OK Indicates that the input address passed a security test. For example, the address is permitted to relay mail.

$discard Indicates that the input address failed some security test and the e-mail message should be discarded.

NOTE Neither OK, discard, nor error, which is discussed in a second, are declared in Commands like real mailers. But the Sendmail documentation refers to them as “mailers” and so we do.

The $$OK and $$discard are used in spam control and security. You will see more of them in later chapters. The $$discard silently discards the mail and does not return an error message to the sender. The $$error mailer is another mailer that handles undeliverable mail, unlike $$discard, it returns an error message to the sender. The template syntax used with the $$error is more complex than the syntax of either $$OK or $$discard. That syntax is shown below:

```
$error $$dsn-code $:message
```

To properly process an error message, the mailer must be $$error. $:message field contains the text of the error message that you wish to send. The $$dsn-code field is optional. If it is provided, it appears before the message and must contain a valid DSN error code as defined by RFC 1893 (“Mail System Status Codes”) or a valid Sendmail keyword. Table 8.5 lists the valid Sendmail error code keywords and their meanings.

# Table 8.5 Sendmail Error Code Keywords

| Keyword | Meaning |
| --- | --- |
| config | An internal configuration error or routing loop was detected. |
| nohost | The host portion of the sender or recipient address is invalid. |
| nouser | The user portion of the sender or recipient address is invalid. |
| protocol | Network delivery failed.