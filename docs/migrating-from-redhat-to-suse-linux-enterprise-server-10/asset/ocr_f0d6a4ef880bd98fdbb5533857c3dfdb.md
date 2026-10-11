The following figure, taken from the original Postfix documentation, shows a rough summary of the modularization of Postfix.

Modules that are not covered at this stage are in /usr/share/doc/packages/postfix/html/OVERVIEW.html.

![](bbox=[0.09, 0.25, 0.89, 0.45])

Individual Postfix processes are represented in the diagram by ellipses. Dark squares stand for lookup tables and light squares represent mail queues or mailboxes.

For security reasons, Postfix works with four mail queues. For every mail queue, there is a directory bearing the same name under /var/spool/postfix/.

The functions of the queues and the Postfix files are described in

+   - Process of Inbound Email
+   - Process of Outbound Email
+   - Components of the Postfix Program Package