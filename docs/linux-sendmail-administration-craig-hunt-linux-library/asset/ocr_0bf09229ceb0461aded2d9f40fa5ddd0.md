# Table C.5 Mailer Flags

| Name | Function |
|---|---|
| C | Adds @domain to addresses that do not have an @.
| D | Adds a Date: header line to outgoing mail. |
| E | Adds > to message lines that begin with From:
| e | Indicates that this is a resource-intensive mailer. |
| F | Adds a From: header line to outgoing mail. |
| f | Indicates that this mailer allows trusted users to send mail under other names. |
| h | Preserves uppercase in hostnames. |
| I | Indicates that this mailer uses SMTP. |
| L | Limits the line length as required by RFC 821. |
| 7 | Indicates that this is a local mailer. |
| M | Adds a Message-Id: header line to outgoing mail. |
| m | Indicates that the mailer can send to multiple users in one transaction. |
| n | Indicates that Unix-style From: lines should not be used. |
| P | Adds a Return-Path: header to outgoing mail. |
| R | Uses the MAIL From: return-path rather than the return address. |
| r | Indicates that this mailer allows trusted users to send mail under other names. |
| S | Prevents the user ID from being reset before calling the mailer. |
| s | Strips quotes off the address before calling the mailer. |
| U | Indicates that the mailer requires Unix-style From: lines. |
| u | Preserves uppercase in usernames. |