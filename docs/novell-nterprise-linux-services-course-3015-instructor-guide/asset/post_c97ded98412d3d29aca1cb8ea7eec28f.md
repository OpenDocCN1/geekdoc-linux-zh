
## iFolder Benefits

With the lack of local data backup and expanding mobile work forces, companies need a product that provides easy access to personal files stored on the network and a system that automatically synchronizes those files from any location.

iFolder addresses those needs (and others) for the enterprise and the user. It provides the following benefits:

- **Seamless data access.** iFolder stores and synchronizes users’ work in such a way that no matter what client or what location they log in from, their files are available and in the condition that they expect them to be.
- **Data safeguards and data recovery.** When a user saves a file locally, the iFolder client can automatically update data to the iFolder server where it immediately becomes available for an organization’s regular network backup operations.

iFolder also gives Internet Service Providers (ISPs) the ability to offer a user-trusted backup solution for their customers’ critical business or personal data.

- **Reliable data security.** With iFolder encryption, stored data is secure from unauthorized network access.

iFolder encrypts all data before it crosses the Internet and stores it on the Novell iFolder server, keeping it out of the hands of unauthorized users.

- **Productive mobile users.** iFolder does away with version inconsistency, making it simple for users to access the most up-to-date version of their documents from any connected desktop, laptop, or Web browser.

In preparation to travel or work from home, users no longer have to copy needed data to their laptops from various desktop and network locations.

The iFolder client can automatically update users' laptops and desktops with the most current versions of their files. Even if a user loses a laptop, all those files can still be accessed with any computer connected to the Internet.

- **Cross-platform support.** The iFolder server integrates with either the Apache Web server on NetWare® and Linux or the Microsoft Internet Information Servers (IIS) Web server on Windows 2000.

Additionally, the iFolder's LDAP support for user authentication lets you leverage Novell eDirectory™ on NetWare, Linux, and Windows 2000 servers, or Microsoft Active Directory™ on Windows 2000 servers.

- **Simple data and account management.** iFolder is designed to allow for easy setup and management by network administrators.

The iFolder server can be managed from any location using a standard Web browser. With its automatic file updates, synchronization, and encryption, iFolder also frees up IT departments from routine maintenance tasks.

Network administrators also have the option to manage Novell iFolder accounts using eDirectory or Microsoft Active Directory (on Windows 2000 servers only).

- **Large-scale deployment.** One of the key features of iFolder is its ability to scale to a large and growing environment. You can install iFolder on multiple servers, allowing your iFolder environment to grow with your business.

There is no practical limit to the number of iFolder servers that you can have in your iFolder network—a single iFolder server handles up to 10,000 user accounts. In turn, each of these servers together acts as 1 system.

Because iFolder takes care of redirecting user authentication requests to the correct iFolder server, the login procedure is a seamless experience for the user.

Plus, as your iFolder network grows, your management costs stay the same, because the management of all iFolder servers is centralized through the iFolder Management console.

- **Benefits for users.** Novell iFolder provides the following benefits to users:
    - Guards against local data loss by automatically backing up your local files to the iFolder server and your multiple workstations.
    - Automatically updates files across the machines you regularly use (work, laptop, home) making the view of data the same on all machines.
    - Lets you keep files in a local directory (such as My Documents), so you use them the same way you always have.
    - Lets you access your files anywhere on the road using a web browser.
    - Tracks and logs changes made while you work offline and synchronizes those changes when you go online.
    - With encryption enabled, protects data as it travels across the wire and while stored on the iFolder server.

## iFolder Features

In addition to the benefits provided by iFolder, the following are key features that make iFolder an effective personal file access and synchronization service:

- **Support for the following network operating systems:**
    - NetWare 5.1 with Support Pack 5 or later
    - NetWare 6.0 with Support Pack 2 or later
    - NetWare 6.5 or later
    - Microsoft Windows 2000 Server with Service Pack 3 or later
    - Red Hat® Linux AS 2.1 Enterprise
    - SuSE® SLES 8
- **LDAP support for the following:**
    - Novell eDirectory for NetWare, Windows 2000, and Red Hat or SLES 8 Linux servers
    - Microsoft Active Directory for Windows 2000 servers
- **Large-scale deployment support** using multiple iFolder servers acting as a single system
- **Report generator** for administrators to view statistics on iFolder users and the iFolder system
- **Automatic upgrade** through the Red Carpet™ daemon in NNLS
- **Client support for the following workstation operating systems:**
    - Windows 98/ME
    - Windows NT® 4/2000 Professional
    - Windows XP Home and Professional
- **Concurrent access** to multiple iFolder accounts using Novell NetDrive to map drives to the iFolder server
- **Thin-client support** through Novell NetDrive for Citrix® MetaFrame® servers, Windows 2000 Terminal Server, and ZENworks® OnDemand Services
- **File encryption** across the wire and on the iFolder server to protect user data from unauthorized access
- **Management** of iFolder server and accounts through a Web browser

![](img/d63035f3fce0eaaf97203dde900affb7_16_0.png)

For information about key features of the iFolder client, see the Novell iFolder 2.1 User Guide at http://www.novell.com/documentation.

## iFolder Components

There are 3 software components to iFolder:

- iFolder server software
- iFolder client software
- Java applet

These components work together to provide users with instant access to any iFolder files stored on their local computer from anywhere in the world.

The following illustrates how the iFolder server is accessed from different computers or locations:

![](img/d63035f3fce0eaaf97203dde900affb7_17_0.png)

At the center of the iFolder architecture is the iFolder server and storage components. These key components let you access and synchronize network files on the iFolder server from inside the firewall (from your office computer) or from outside the firewall (from a laptop, home computer, or kiosk).

Currently, the iFolder Java Applet is only compatible with Internet Explorer.

All users connect to the iFolder server through a small iFolder client to synchronize and store their data. Users can install the client on any Windows workstation. This sets up an iFolder directory on their local drive.

When users save or update any files to this local directory, the files are automatically delivered to the Novell iFolder server, and then synchronize to their other computers that have the iFolder client installed.

Using the iFolder Java Applet on Internet Explorer, users can also access their files by visiting the company's iFolder web site, and entering their ID, password, and pass phrase (the pass phrase enables the encryption of the files).

You can allocate space to each user by using a default policy, or by modifying a user's individual account.

Files stored on the iFolder server are encrypted and protected by the company's backup and storage procedures.

Users authenticate to the iFolder server through LDAP v3. The LDAP authentication server can be the Linux server that the iFolder product was installed on, or any other LDAP-enabled directory (such as eDirectory) that supports LDAP v3.

To authenticate, users must know their username and password and the pass phrase used for encryption. This information is verified by the iFolder server against the LDAP server.

LDAP authentication can be done using SSL on port 636 or clear text on port 389. It is important to realize that the LDAP server is not accessed by the iFolder client directly, but by an LDAP call from the iFolder server.

iFolder is both an intranet and an Internet solution that will work with any LAN or Internet connection.
