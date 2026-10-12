![](bbox=[0.13, 0.15, 0.26, 0.22])

To learn more about Linux security, consult the Linux Security HOWTO at http://metalab.unc.edu/pub/Linux/docs/HOWTO/Security-HOWTO. Another good resource is the Linux Administrator's Security Guide, which you can read online at http://www.securityportal.com/lasg/.

# Establishing a Security Policy

The first step in securing your Linux system is to set up a security policy. The security policy is your guide (or rules) to what you enable users (as well as visitors over the Internet) to do on the Linux system. The level of security depends on how you use the Linux system and how much is at risk if someone gains unauthorized access to your system.

If you are a system administrator for Linux systems at an organization of any sort, you probably want to involve the management as well as the users in setting up the security policy. Obviously, you cannot create such an imposing policy that no one can do any work on the system. On the other hand, if the users are creating or using data that's valuable to the organization, you have to set up a policy that aims to protect the data from disclosure to outsiders. In other words, the security policy should strike a balance between the users' needs and the need to protect the system.

For a standalone Linux system or a home system that you occasionally connect to the Internet, the security policy can be just a listing of the Internet services that you want to run on the system and the user accounts you plan to set up on the system. For any larger organization, you probably have one or more Linux systems on a LAN connected to the Internet — preferably through a firewall (a device that controls the flow of Internet Protocol (IP) packets between the LAN and the Internet). In such cases, the security policy typically addresses the following areas:

+   - *Authentication:* Who gets access to system? What is the minimum length and complexity of passwords? How often must you change passwords? How long can a user be idle before that user is logged out automatically?
+   - *Authorization:* What can different classes of users do on the system? Who can have the root password?
+   - *Data Protection:* What data has to be protected? Who has access to the data?
+   - *Internet Access:* What are the restrictions on users (from the LAN) accessing the Internet? What Internet services (such as Web, Internet Relay Chat, and so on) can the users access? Are incoming e-mails and attachments scanned for viruses? Is there a network firewall?