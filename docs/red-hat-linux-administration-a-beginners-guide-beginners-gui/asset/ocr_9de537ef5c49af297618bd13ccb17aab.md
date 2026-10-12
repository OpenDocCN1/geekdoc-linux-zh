While a POP client that is kept online for long periods of time can be configured to poll the server occasionally for new mail, IMAP avoids this problem altogether. A client connected to an IMAP server can be notified directly of any new mail that arrives.

Just in case the basic status indicators of read/unread, answered, important, and so on, aren’t sufficient for your needs, IMAP allows user-defined Status flags. This means you can mark messages in ways that are uniquely meaningful to you and your needs.

IMAP can even support non–e-mail applications. For example, you may set up a documentation repository as an anonymous read-only IMAP folder. This could then be available to your entire company and accessed with any IMAP client.

When the client performs its initial handshake with the server, it negotiates which capabilities are supported by both machines, and which are not. This structure makes it easy to add optional features to IMAP gradually, without a major upheaval to the protocol. For example, during the initial handshake, clients and servers can negotiate support for start-TLS–style encrypted connections, something that was not in the original IMAP specification.

For those with pay-by-the-minute Internet connections, or other specialized circumstances that make POP’s “offline” mode seem attractive, IMAP offers a “disconnected” mode. In this mode, all new mail is copied down to the client for local processing. Deletions and status changes are kept recorded by the client, and synced back to the server next time you connect. While this trades off connection time for bandwidth usage, it will still maintain many of the other advantages of using IMAP, such as a centralized mail store accessible by multiple clients, or custom status flags.

# ## Ask the Expert

> **Q:** Wow! IMAP sounds so cool. Are there any issues to consider when installing all these features?

> **A:** Even though the IMAP specification supports a large set of features, you’re still dependent on these features being implemented in your server and client software. Not all client software supports all of the more esoteric or recently proposed features of the protocol. Some server or mailbox configurations can also limit the features available for use.