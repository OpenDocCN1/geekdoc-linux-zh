![](bbox=[0.35, 0.09, 0.68, 0.47])

**Figure 4-10** This screen shows the unlocking tool anySIM.

# ## PDA Attacks

There are different security issues that relate to PDAs. The largest of these is the theft of the device itself. The best precaution to overcome this threat is to secure the data on the device in standalone mode and to password-protect the device.

The second-largest security risk related to PDAs is viruses. Mobile code vulnerabilities such as Java and ActiveX exploits are also a threat, but only affect PDAs that can access the Internet.

PDAs that use wireless services or wireless ports are also vulnerable to wireless attacks. The best solution to protect PDAs from wireless attacks is to install a VPN client on the user’s PDA. While it protects the wireless transmission session, VPN also protects the sensitive data being transmitted. Encryption is another solution to protect data and links that are used to connect to remote systems on the Internet.

Some specific attacks are described in the following sections.

# ### ActiveSync Attacks

Affects: Windows Mobile Pocket PC

Windows Mobile Pocket PC is vulnerable to ActiveSync attacks. ActiveSync synchronizes Windows-based PDAs and smartphones with a desktop computer. ActiveSync typically requires a physical connection to a desktop PC through a cradle. It requires a password to be entered, but permits unlimited password attempts. This allows an attacker to perform brute-force and dictionary attacks.

If a user saves a mobile password on the desktop, an attacker, after gaining access to the desktop, can also access the ActiveSync password along with any other information on the desktop. The attacker can steal private information or unleash malicious code, such as a keylogger or spyware.

# ### HotSync Attacks

Affects: Palm OS

Palm devices are vulnerable to HotSync attacks. HotSync synchronizes the information between a Palm device and a desktop PC. The synchronized information includes e-mails, contacts, calendar items, tasks, and notes.