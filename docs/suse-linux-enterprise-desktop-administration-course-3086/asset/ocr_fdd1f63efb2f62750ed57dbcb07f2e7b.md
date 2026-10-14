+   - **Account expired**—An administrator can set an expiration time for a specific user account. If that user tries to log in after that time has passed, the user gets a message that the account has expired and cannot be used to log in.

During a successful authentication, pam_windbind acquires a ticket granting ticket (TGT) from the Kerberos server of Active Directory and stores it in the user’s credential cache. It also renews the TGT in the background without requiring any user interaction.

SUSE Linux Enterprise Desktop 10 supports local home directories for AD users. If configured through YaST, as described in “Configure a Linux Client for Active Directory,” user homes are created at the first login of a Windows (AD) user to the Linux client.

These home directories look and feel entirely the same as standard Linux user home directories and work independently of the AD domain controller.

Using a local user home, it is possible to access a user’s data on this local machine, even when the AD server is disconnected, provided the Linux client has been configured to perform offline authentication.

**Offline Service and Policy Support** Users in a corporate environment must have the ability to become roaming users, so they can, for example, switch networks or even work disconnected for some time.

To enable users to log in to a disconnected machine, extensive caching was integrated into the windbind daemon. The windbind daemon enforces password policies even in the offline state. It tracks the number of failed login attempts and reacts according to the policies configured in Active Directory.

Offline support is disabled by default and must be explicitly enabled in the YaST Domain Membership module.

As in Windows, when the domain controller has become unavailable, the user can still access network resources (other than the AD server itself) with valid Kerberos tickets that have been acquired before losing the connection.

Password changes cannot be processed unless the domain controller is online. While disconnected from the AD server, a user cannot access any data stored on this server.

When a workstation has become disconnected from the network entirely and attaches to the corporate network again later, SUSE Linux Enterprise Desktop 10 acquires a new Kerberos ticket as soon as the user has locked and unlocked the desktop.

# Configure a Linux Client for Active Directory

Before your client can join an AD domain, you must make some adjustments to your network setup to ensure a flawless interaction of client and server. These adjustments affect:

+   - DNS
+   - NTP
+   - DHCP
+   - Firewall
+   - AD Account

![](bbox=[0.95, 0.653, 1.0, 0.708])