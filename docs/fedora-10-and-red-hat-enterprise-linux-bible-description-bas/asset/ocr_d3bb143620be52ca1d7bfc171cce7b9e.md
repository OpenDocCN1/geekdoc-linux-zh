# Chapter 2: Installing Fedora 45

as John W. Parker or Alan Bourne). Then you type your password in the Password text box and again in the Confirm Password text box. Click Forward.

If some sort of network authentication is used, such as LDAP, Kerberos, or SMB authentication, you can click the Use Network Login button. See "Enabling Authentication" sidebar for information on choosing different authentication types.

+   - Date and Time — Set the date and time, and enable the network time protocol to keep your system properly set. Click Forward.

+   - Hardware Profile — The Smolt hardware profiler runs to gather and display all kinds of information about your hardware. Select Sent Profile if you agree to have this information sent to the Fedora Project. Click Forward.

Firstboot is complete. Finish to continue. You may need to reboot. See Chapter 3 for a description of how to log in to Fedora and start learning how to use Linux.

When Fedora starts up the next time, it will boot up to a login prompt. A graphical boot screen is displayed (instead of a scrolling of lists starting up).

# Enabling Authentication

In situations, you will enable shadow passwords and MD5 passwords (as selected by default) to authenticate users who log in to your computer from password and shadow files. To change that behavior, you can select the Use Network Login button during the User setup during Firstboot.

The shadow password file prevents access to encrypted passwords. MD5 is an algorithm used to encrypt passwords in Linux and early UNIX systems. It replaces an algorithm called crypt, which was used with early UNIX systems. When you enable MD5 passwords, your users can have longer passwords that are harder to break than those encrypted with crypt. You can also use SHA512 or SHA256 for encrypting passwords.

If you are on a network that supports one of several different forms of network-wide authentication, you may choose one of the following (on the Authentication tab):

+   - Enable Kerberos Support. Check this box to enable network authentication services through Kerberos. After enabling Kerberos, you can add information about a Kerberos Realm (a group of Kerberos servers and clients), KDC (a computer that issues Kerberos tickets), and Admin server (a server running the Kerberos kadmind daemon).

+   - Enable LDAP Support — If your organization gathers information about users, you can click this box to search for authentication information in an LDAP server. You can enter the LDAP server name and optionally an LDAP distinguished name to look up the user information your system needs.

+   - Enable Smart Card Support — Tick this box to allow users to log in