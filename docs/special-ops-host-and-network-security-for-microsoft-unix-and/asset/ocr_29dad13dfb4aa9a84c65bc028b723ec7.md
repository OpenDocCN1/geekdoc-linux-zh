# Table 7.13 Diagnostics Logging Categories for Exchange 2000 Servers

| Category | Explanation |
|---|---|
| ExchangeS | Mailbox | Logons | Tracks access to mailboxes |
| | Access Control | Logs events when users attempt to access a mailbox to which they have no permissions or insufficient permissions |
| ExchangeS | Mailbox | Send As | Logs events when users use the Send As permission |
| ExchangeS | Public Folder | Logons | Tracks access to the public folder store |
| ExchangeS | Public Folder | Access Control | Logs events when users attempt to access a public folder to which they have no permissions or insufficient permissions |
| ExchangeS | System | Virus Scanning | Logs events related to virus scanning programs that are AVAPI 2.0-compliant |
| IMAP4 | Connections | Logs information about IMAP4 client connections such as IP address |
| IMAP4 | Authentication | Logs information about IMAP4 client authentication |
| POP3Svc | Connections | Logs information about IMAP4 client connections such as IP address |
| POP3Svc | Authentication | Logs information about POP3 client authentication |

Although these are not the only categories of events you can log with Exchange 2000, I consider these to be the bare essential events from a security perspective. Many organizations have requirements for logging additional information such as X,400 MTA connections, and transport-related events. The categories in the preceding table should be set to at least minimum.

When you are scanning your event logs looking for possible intrusions or things that don't look right, the event IDs in Table 7.14 may be helpful. These are by no means the events you should be looking at, but they will help you narrow down the events that indicate when a user is accessing the store.

![](bbox=[0.706, 0.946, 0.93, 0.966])