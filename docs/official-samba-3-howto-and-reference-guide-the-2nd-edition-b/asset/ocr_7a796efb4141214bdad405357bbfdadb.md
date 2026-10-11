# **NOTE**

![](bbox=[0.08, 0.17, 0.13, 0.28])

Algin Technology LLC provide a commercial tool that makes it possible to promote a Windows NT4 standalone server to a PDC or a BDC, and also permits this process to be reversed. Refer the the Algin<sup>a</sup> web site for further information.

> a<http://utools.com/UPromote.asp>

Samba-3 servers can readily be converted to and from domain controller roles through simple changes to the `smb.conf` file. Samba-3 is capable of acting fully as a native member of a Windows 200x server Active Directory domain.

For the sake of providing a complete picture, MS Windows 2000 domain control configuration is done after the server has been installed. Please refer to Microsoft documentation for the procedures that should be followed to convert a domain member server to or from a domain control, and to install or remove active directory service support.

New to Samba-3 is the ability to function fully as an MS Windows NT4-style domain controller, excluding the SAM replication components. However, please be aware that Samba-3 also supports the MS Windows 200x domain control protocols.

At this time any appearance that Samba-3 is capable of acting as a *domain controller* in native ADS mode is limited and experimental in nature. This functionality should not be used until the Samba Team offers formal support for it. At such a time, the documentation will be revised to duly reflect all configuration and management requirements. Samba can act as a NT4-style domain controller in a Windows 2000/XP environment. However, there are certain compromises:

+   - No machine policy files.
+   - No Group Policy Objects.
+   - No synchronously executed Active Directory logon scripts.
+   - Can't use Active Directory management tools to manage users and machines.
+   - Registry changes tattoo the main registry, while with Active Directory they do not leave permanent changes in effect.
+   - Without Active Directory you cannot perform the function of exporting specific applications to specific users or groups.

# 4.3.2 Preparing for Domain Control

There are two ways that MS Windows machines may interact with each other, with other servers, and with domain controllers: *either as standalone systems*, more commonly called