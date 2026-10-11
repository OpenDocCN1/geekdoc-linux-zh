# 25.4.2 Windows NT4/200x

The tools that may be used to configure these types of controls from the MS Windows environment are the NT4 User Manager for Domains, the NT4 System and Group Policy Editor, and the Registry Editor (regedt32.exe). Under MS Windows 200x/XP, this is done using the MMC with appropriate “snap-ins,” the registry editor, and potentially also the NT4 System and Group Policy Editor.

# 25.4.3 Samba PDC

With a Samba domain controller, the new tools for managing user account and policy information include: **smbpasswd**, **pdbedit**, **net**, and **rpcclient**. The administrator should read the man pages for these tools and become familiar with their use.

# 25.5 System Startup and Logon Processing Overview

The following attempts to document the order of processing the system and user policies following a system reboot and as part of the user logon:

+   Network starts, then Remote Procedure Call System Service (RPCSS) and multiple universal naming convention provider (MUP) start.

+   Where Active Directory is involved, an ordered list of GPOs is downloaded and applied. 
+   The list may include GPOs that:

+   Apply to the location of machines in a directory.

+   Apply only when settings have changed.

+   Depend on configuration of the scope of applicability: local, site, domain, organizational unit, and so on.

No desktop user interface is presented until the above have been processed.

+   Execution of startup scripts (hidden and synchronous by default).

+   A keyboard action to effect start of logon (Ctrl-Alt-Del).

+   User credentials are validated, user profile is loaded (depends on policy settings).

+   An ordered list of user GPOs is obtained. The list contents depends on what is configured in respect of:

+   Is the user a domain member, thus subject to particular policies?

+   Loopback enablement, and the state of the loopback policy (merge or replace).

+   Location of the Active Directory itself.

+   Has the list of GPOs changed? No processing is needed if not changed.

+   User policies are applied from Active Directory. Note: There are several types.