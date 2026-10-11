c.  The pickup daemon transfers the message from the maildrop directory and forwards it to the cleanup daemon.

3.  The e-mail message, regardless of whether it originated remotely or on the local system, is then processed by the cleanup daemon.

4.  The cleanup daemon places the e-mail message in the incoming queue, which is also `/var/spool/postfix`.

5.  The cleanup daemon notifies the Queue Manager daemon (`qmgr`) that a message has been added to the incoming queue.

6.  The `qmgr` daemon moves the e-mail message to one of five message queues, all of which are located in `/var/spool/postfix`:

a.  **incoming**  This queue contains incoming messages that have been processed by the cleanup daemon.

b.  **active**  This queue contains messages that arrived intact, were processed correctly, and are ready to be forwarded on to the next MTA or MDA.

c.  **hold**  This queue contains messages whose delivery, for some reason, has been put on hold.

d.  **deferred**  This queue contains messages that could not be delivered on the first attempt. The `qmgr` daemon will wait a while; then it will make several more delivery attempts.

e.  **corrupt**  This queue contains messages that were damaged somewhere in transit and are no longer readable.

7.  The `qmgr` daemon then invokes the trivial-rewrite daemon, which identifies the next MTA or MDA to which the message should be sent.

8.  The `qmgr` daemon then passes the message to the appropriate delivery agent. If the message is intended for a local user account, the local agent is used. If the agent intended for another MTA or an MDA, the smtp agent is used.

9.  The selected agent transfers the e-mail message to the appropriate system.

•  **qmail**  The qmail MTA is also a modular MTA daemon that is frequently used as a replacement for sendmail. The qmail MTA is unique in that it was designed from the ground up with security in mind. Essentially, its modular architecture is composed of mutually untrusting components. This means each module in the MTA (such as the SMTP listener) will use a set of credentials that are unique to it. No two modules use the same credentials. Many administrators consider qmail, like postfix, easier to manage than sendmail. However, it’s not the default MTA used by any Linux distribution because it has components that are covered by a proprietary licensing agreement. In spite of this, qmail is greatly loved by those who use it. My niece is married to a system admin and he swears by qmail. You need to be aware that two additional mail protocols are implemented by qmail:

•  **Quick Mail Queueing Protocol (QMQP)**  Allows the sharing of e-mail queues among different MTAs