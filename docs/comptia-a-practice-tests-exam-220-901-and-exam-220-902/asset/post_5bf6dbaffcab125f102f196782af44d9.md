
without needing to use a key, a card, or any other security device. Using mantraps, which are devices such as small rooms that limit access to one or a few individuals, is a great way to stop tailgating.

### 8. B
Adding Roberts to the Administrators group will certainly work, but it's not the recommended approach. Since members of the Administrators group have such power, they can inadvertently do harm (such as accidentally deleting a file that a regular user could not). To protect against this, the practice of logging in with an Administrators group account for daily interaction is strongly discouraged. Instead, system administrators should log in with a user account (lesser privileges) and change to the Administrators group account (elevated privileges) only when necessary.

### 9. A
Biometric authentication requires identification of a physical feature of the user, such as a fingerprint or facial scan. DNA is considered a form of biometric authentication, but it's not commonly used today with mobile devices. (Imagine your phone needing to collect blood or saliva to authenticate you—no thanks!)

### 10. D
If you're using FAT32 and want to change to NTFS, the convert utility will allow you to do so. For example, to change the E: drive to NTFS, the command is `convert e: /FS:NTFS`.

### 11. D
When there are conflicting NTFS permissions, generally they are combined, and the most liberal is granted. The exception to that is when there is an explicit Deny. That overrides any allowed permissions.

### 12. C
Microsoft wanted to create a group in Windows that was not as powerful as the Administrators group, which is how the Power Users group came into being. The idea was that membership in this group would be given read/write permission to the system, allowing members to install most software but keeping them from changing key operating system files.

### 13. C
When assigning user permissions, follow the principle of least privilege; give users only the bare minimum that they need to do their job. Assign permissions to groups rather than users, and make users members of groups (or remove them from groups) as they change roles or positions.

### 14. D
Placing an unauthorized router with a seemingly legitimate configuration is specifically known as an evil twin. Those can lead to man-in-the-middle attacks, which involve clandestinely placing something (such as a piece of software or a rogue router) between a server and the user, and neither the server’s administrator nor the user is aware of it. The man-in-the-middle intercepts data and then sends the information to the server as if nothing is wrong. The man-in-the-middle software may be recording information for someone to view later, altering it, or in some other way compromising the security of your system and session.

### 15. B
Companies normally generate a huge amount of paper, most of which eventually winds up in dumpsters or recycle bins. Dumpsters may contain information that is highly sensitive in nature, and attackers may seek it out by practicing Dumpster diving. In high-security and government environments, sensitive papers should be either shredded or burned.

### 16. B, D
You should rename the default account and always require strong passwords. In Windows, you are unable to disable the Administrator account or remove it from the Administrators group.

### 17. A
A virtual private network (VPN) is a private network connection that occurs through a public network. VPNs make use of tunneling, which sends private data across a public network by placing (encapsulating) that data into other packets. Even though a VPN is created through the Internet or other public networks, the connection logically appears to be part of the local network.

### 18. B, D
NTFS permissions affect users regardless of whether they are at the local computer or accessing the resource across the network. They can also be applied to individual files, whereas share permissions can be applied only to folders. One set of permissions is not inherently more restrictive than the other, as either type can be used to deny access in a given situation (at least when accessing across the network).

### 19. B
An ID badge is worn by employees to identify them. Some companies use different colored badges to indicate different functions or security privileges. Most ID badges have a picture of the user on them to prevent unauthorized use.

### 20. C
A locator app is what you need. Apple supplies a free app called Find My iPhone that, together with iCloud, allows multiple mobile devices and Macs to be located if powered on and attached to the Internet (via 4G, 3G, Wi-Fi, Ethernet, and so on). The app allows the device to be controlled remotely to lock it, play a sound (even if audio is off), display a message, or wipe it clean.

### 21. A
File systems such as NTFS, and security devices such as firewalls, can track security in access control lists (ACLs). ACLs can hold permissions for local users and groups, and each entry in the ACL can also specify what type of access is given. This allows a great deal of flexibility in setting up a network.

### 22. C, D
The four common file attributes are Read-only, Archive, System, and Hidden (remember the acronym RASH). They can be implemented on FAT32 or NTFS volumes and changed by anyone with proper access. On NTFS volumes, you can also compress or encrypt files as part of advanced attributes. At a command prompt, the attrib command is used to change attributes. In Windows, right-click the file, choose Properties, and look for Attributes on the General tab.

### 23. A
The systems are not up-to-date and therefore are more vulnerable to attacks. These systems are considered noncompliant systems. It’s a violation of security best practices to fail to keep all software on your network up-to-date.

### 24. B
Acceptable use policies (AUPs) describe how the employees in an organization can use company systems and resources, both software and hardware. This policy should also outline the consequences for misuse. In addition, the policy (also known as a use policy) should address the installation of personal software on company computers and the use of personal hardware such as USB devices.

### 25. B
BitLocker allows you to use drive encryption to protect files—including those needed for startup and logon. This is available only with more complete editions of Windows 8 (Pro and Enterprise), Windows 7 (Enterprise and Ultimate), and Windows Vista (Enterprise and Ultimate). For removable drives, BitLocker To Go provides the same encryption technology to help prevent unauthorized access to the files stored on them.

### 26. C
Spyware differs from other malware in that it works—often actively—on behalf of a third party. Rather than self-replicating, like viruses and worms, spyware is spread to machines by users who inadvertently ask for it. The users often don't know they have asked for it but have done so by downloading other programs, visiting infected sites, and so on. The spyware program monitors the user's activity and responds by offering unsolicited pop-up advertisements (sometimes known as adware), gathers information about the user to pass on to marketers, or intercepts personal data such as credit card numbers.

### 27. C
When creating user accounts, follow the principle of least privilege: give users only the permissions they need to do their work and no more. This is especially true with administrators. Users who need administrative-level permissions should be assigned two accounts: one for performing nonadministrative, day-to-day tasks and the other to be used only when performing administrative tasks that specifically require an administrative-level user account. Those users should be educated on how each of the accounts should be used.

### 28. A, C
Password attacks occur when an account is attacked repeatedly. This is accomplished by using applications known as password crackers, which send possible passwords to the account in a systematic manner. Two types of password attacks are brute-force and dictionary attacks.

### 29. C
All the options will increase the security of an iPhone. For
