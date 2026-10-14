**Table 23-1: (continued)**

| Program | Description |
|---|---|
| qmgr | Processes messages in the incoming queue, determining where and how they should be delivered and spawning programs to deliver them |
| sendmail | Provides a sendmail-compatible interface for programs to send messages to the maildrop queue |
| showq | Reports Postfix mail queue status |
| smtp | Forwards messages to external mail hosts using the SMTP |
| smtpd | Receives messages from external mail hosts using the SMTP |
| trivial-rewrite | Receives messages from the cleanup program to ensure header addresses are in a standard format for the qmgr program; also used by the qmgr program to resolve remote host addresses |

Depending on what the Postfix email server is processing, you may see any of these programs running at any given time. Each program runs only when it’s needed by the overall Postfix mail process.

# Postfix Message Queues

Unlike some other MTA packages, Postfix uses several message queues for managing email messages as they are processed. Each message queue contains messages in a different message state in the Postfix system. Table 23-2 lists the message queues that are used by Postfix.

**Table 23-2: Postfix Message Queues**

| Queue | Description |
|---|---|
| maildrop | New messages waiting to be processed, received from local users |
| incoming | New messages waiting to be processed, received from remote hosts, as well as processed messages from local users |
| active | Messages that are ready to be delivered by Postfix |
| deferred | Messages that have failed on an initial delivery attempt and are waiting for another attempt |
| flush | Messages that are destined for remote hosts that will connect to the mail server to retrieve them |
| mail | Delivered messages stored for local users to read |

If the Postfix system should be shut down at any time, messages remain in the last queue where they were placed. When Postfix is restarted, it will automatically begin processing messages from the queues.