# 810 CHAPTER 23 SAMBA: LINUX AND WINDOWS FILE AND PRINTER SHARING

passwd chat The script Samba uses to converse with the passwd program. If this script is not followed, Samba does not change the password. Used only when unix password sync (810) is set to YES.

Default: *new<password>* %n\n*new<password>* %n\n*changed*
Ubuntu: *Enter\new\*password:* %n\nRetype\new\*password:* %n\n*password*updatedsuccessfully*.

passwd program The program Samba uses to Linux passwords. Samba replaces %u with the user's username.

Default:
Ubuntu: /usr/bin/passwd %u

security Specifies if and how clients transfer user and password information to the server. Choose one of the following:

USER: Causes Samba to require a username and password from Windows users when logging in on Samba server. With this setting you can use

+   * username map (page 811) to map Samba usernames to Linux usernames
* encrypt passwords (page 808) to encrypt passwords (recommended)
* guest account (page 809) to map users to the guest account

SHARE: Causes Samba not to authenticate clients on a per-user basis. Instead, Samba uses the Windows NT9 setup, in which each share can have an individual password for either read or full access. This option is not compatible with more recent versions of Windows.

SERVER: Causes Samba to use another SMB server to validate usernames and passwords. If the remote validation fails, the local Samba server tries to validate usernames and passwords as security were set to USER.

DOMAIN: Samba passes an encrypted password to a Windows domain controller for validation. The workgroup parameter (page 808) must be properly set in smb.conf for DOMAIN to work.

ADS: Instructs Samba to use an Active Directory server for authentication, allowing a Samba server to participate in a native Active Directory member. (Active Directory is the centralized information system that Windows 2000 and later use. It replaces Windows Domains, which was used by Windows NT and earlier.)

Default: USER

unix password YES causes Samba to change a user's Linux password when the associated sync changes the encrypted Samba password.

Default: NO
Ubuntu: YES

update YES allows users to migrate from cleartext passwords to encrypted passwords-encrypted logging in on the server and using smbpasswd. To migrate users, set to YES and