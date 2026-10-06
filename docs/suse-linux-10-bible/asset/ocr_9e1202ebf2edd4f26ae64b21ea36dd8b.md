# OpenLDAP

The LDAP server stores the virtual domain information, aliases, address books (both personal to the user and the global address book), and user accounts. It is the most important part of your SLOX environment and defines the profile of your SLOX server. You should routinely back up your LDAP server as well as the mail store when deciding what to save.

Whenever a user logs in, the LDAP server is queried multiple times for the user authentication data and user settings and to load up the server configuration for the duration of the session.

# Netline Servlets

The Netline Servlets provide the groupware functionality of SLOX. This is where the very important WebDAV (Web-Based Distributed Authoring and Versioning) interface is presented to the clients. During the writing of the book, Netline has released an open source version of its application environment. For more information on the Netline program, go to www.open-xchange.org. This is great news because it means the functionality and scalability of the Netline servlets we will hope, increase dramatically in a short space of time.

> As all the groupware services are Java servlets, you will see at least one Java process spawn when any groupware activity takes place.

# WebDAV

Most of the groupware data is stored and queried over WebDAV. This is only for the i/oSLOX connectors (which we talk about later in the chapter). If you have any applications that want to interface with SLOX, you can access calendars, tasks, and projects through a WebDAV interface.

WebDAV is a protocol that allows you to access and query files over HTTP, very much like a mixture of FTP and HTTP. Most vendors have embraced this technology, it provides an excellent opportunity for third-party application vendors, or to write bolt-applications that can talk to SLOX directly. For example, we had a customer who wanted to tie in a student database into the user's calendars directly for their timetables. This is all possible through the WebDAV interface, which most operating systems support very well.

# Cyrus Postfix

All mail-based services are provided by Postfix and Cyrus, both very scalable and reliable mail services.

Cyrus and Postfix both rely on the user data stored in LDAP to function correctly. Any user who wants to make an Internet Access Protocol (IMAP) connection must exist in the LDAP server to be allowed access to any other SLOX service.