# CHAPTER 24 Samba

both platforms. Users may need to work in heterogeneous environments and may need access to the different platforms for seamless as possible for various reasons. It is useful to make working in such environments as possible without having to worry about users' needing to reauthenticate separately on the different platforms, worry about cached passwords that do not match between servers, and other issues.

Relative to Samba, several options are available for handling username and password issues in heterogeneous environments, including the following:

+   - Pluggable authentication modules (PAMs) Allow you to authenticate users against a DC. This means you still have two lists—local and one on the DC—but your users keep track of their passwords only on the Windows system.

+   - Samba as a DC Allow you to keep all your logins and passwords on the Linux system, while all your Windows authenticate with Samba. When Samba is used with a Lightweight Directory Access Protocol (LDAP) back-end for this, you will have a scalable and extensible solution.

+   - Custom script Allows you to use your custom script. For sites with a well-established system for maintaining logins and passwords, it isn't unreasonable to come up with a custom script. This can be done using a scripting language with good code-platform support. Such scripts can be coaxed to allow the Security Access Manager (SAM) to update the DC's password list. For example, a Perl or Python script on the Linux side can communicate with a Perl or Python script on the Windows side to keep accounts synchronized.(Both Perl and Python have been successfully ported to work on Windows platforms through various mechanisms.)

In the worst case, you can always maintain the username and password databases of the different platforms by hand (which some early system admins indeed have to do), but this is error-prone and not much fun to manage.

# Encrypted Passwords

Windows-based systems use encrypted passwords when communicating with the DC and any server requiring authentication (including Linux and Samba). The encryption algorithm used by Windows is different from UNIX's, however, and therefore, is not compatible.

Here are your choices for handling this conflict:

+   - Edit the Registry on Windows clients to disable the use of encrypted passwords. The Registry entries that need to be changed are listed in the docs in the Samba package. As of version 3 of Samba, this option is no longer necessary.

+   - Configure Samba to use Windows-style encrypted passwords.