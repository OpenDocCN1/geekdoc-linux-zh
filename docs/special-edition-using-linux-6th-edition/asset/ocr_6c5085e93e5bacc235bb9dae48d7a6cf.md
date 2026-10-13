can walk out to the mailbox in his front yard or drive to the location of a post office box. Similarly, the recipient of email can use different methods of collecting his or her messages.

# A POP SERVER

Post Office Protocol (POP) provides a way for end users to retrieve their mail. It’s similar to you walking out to your mailbox, collecting the mail, walking back into your house, and sitting down and reading it. Using POP, email is delivered to the email client on your desktop when you indicate that you want to retrieve it. Often, the client desktop is configured to do this each time a dial-up connection is made or at a predetermined time interval. The mail is literally moved from the server to the client.

POP3 requires very little in the way of setup and runs by default in a standard Linux install. POP3 runs from `/etc/inetd.conf`, so access can be controlled with TCP Wrappers if desired. As long as the pop3 entry is listed in `/etc/services` and the pop3 line shows up in `/etc/inetd.conf` (and hasn’t been commented out), you’re already running POP3. You can verify this by inspecting the output of `netstat -an` for a local port 110 that is listening.

# AN IMAP SERVER

An IMAP server behaves much like a POP server, but with one major difference—the IMAP server does not literally transfer the email from the server to the client desktop. It basically creates a “map” for a given user that enables him to read the mail directly on the email server system. The advantages and disadvantages of IMAP versus POP are very similar to the advantages and disadvantages of centralized versus distributed processing.

IMAP, although a different program from POP3, runs out of `/etc/inetd.conf` in exactly the same way as POP3—it just uses port 143 instead of 110. Because IMAP is slightly more powerful, it is also slightly more vulnerable to exploits. If you use IMAP, you will want to use TCP Wrappers to limit access.

# ENABLING POP AND IMAP SERVICES

If not already running, enabling either POP or IMAP service is a very simple task. Each of these protocols is predefined in the `/etc/services` file. The only real requirement is to install the IMAP RPM.

After the RPM is installed, the appropriate daemon is called when requests are detected for either POP or IMAP services on the respective ports, as defined in the `/etc/services` file. That’s all there is to setting up both POP and IMAP services. After they are enabled, email clients can be configured to receive email through this server.

# FETCHMAIL

fetchmail is a specialized type of delivery agent that can download mailbags from an ISP or grab mail from different POP and IMAP servers and deposit it locally.