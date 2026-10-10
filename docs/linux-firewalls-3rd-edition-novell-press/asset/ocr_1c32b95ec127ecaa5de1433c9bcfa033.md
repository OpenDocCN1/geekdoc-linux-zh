# Email (TCP SMTP Port 25, POP Port 110, IMAP Port 143)

Email is a service that almost everyone wants. How mail is set up depends on your ISP, your connection type, and your own choices. Email is sent across the network using the SMTP protocol assigned to TCP service port 25. Email is commonly received locally through one of three different protocols—SMTP, POP, or IMAP—depending on the services your ISP provides and on your local configuration.

SMTP is the general mail protocol. Mail is delivered to the destination host machine, as defined most commonly by the MX record in the DNS for the given domain. The endpoint mail server determines whether the mail is deliverable (addressed to a valid user account on the machine) and then delivers it to the user's local mailbox.

POP and IMAP are mail-retrieval services. POP runs on TCP port 110. IMAP runs on TCP port 143. ISPs commonly make incoming mail available to their customers using one or both of these two services. Both services are usually authenticated by username and password. As far as mail retrieval is concerned, the difference between SMTP and POP or IMAP is that SMTP receives incoming mail and queues it in the user's local mailbox. POP and IMAP retrieve mail into the user's local mail program from the user's ISP, where the mail had been queued remotely in the user's SMTP mailbox at the ISP. Table 4.3 lists the complete client/server connection protocols for SMTP, POP, and IMAP. SMTP also uses specialized delivery mechanisms that your local network might use, such as ETRN, that effectively transfer all mail for a given domain for local processing.

TABLE 4.3

SMTP, POP, and IMAP Mail Protocols

| DESCRIPTION | PROTOCOL | REMOTE ADDRESS | REMOTE PORT | LOCAL IN/OUT | LOCAL ADDRESS | LOCAL PORT | TCP FLAG |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Send outgoing mail | TCP | ANYWHERE | 25 | Out | IPADDR | 1024: 65535 | Any |
| Remote server response | TCP | ANYWHERE | 25 | In | IPADDR | 1024: 65535 | ACK |
| Receive incoming mail | TCP | ANYWHERE | 1024: 65535 | In | IPADDR | 25 | Any |
| Local server response | TCP | ANYWHERE | 1024: 65536 | Out | IPADDR | 25 | ACK |
| Local client query | TCP | POP SERVER | 110 | Out | IPADDR | 1024: 65535 | Any |
| Remote server response | TCP | POP SERVER | 110 | In | IPADDR | 1024: 65535 | ACK |