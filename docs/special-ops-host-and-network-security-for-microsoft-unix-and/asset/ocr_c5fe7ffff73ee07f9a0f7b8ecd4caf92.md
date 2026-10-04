policies that apply to that computer. When a user logs on to Active Directory, Active Directory applies the User configuration of the group policies that apply to that user. Even though the group policies may be housed together, they are applied independently. This independence enables a user's environment to follow him intelligently around the network.

The remaining part of IntelliMirror is the ability to have redirected folders. This means that a user transparently accesses files from a folder that appears to be local but is actually located on a network server.Those files can be backed up, and can be moved around the network without interrupting the user's daily productivity. Offline folders further enable the user to retain a copy of those files locally, which means users can use network files when they are disconnected from the network.

Group policy objects are stored in two places: in the GPT folder SYSVOL on each replicated DC's hard drive, and within the System\Policies container in Active Directory. The System container is not available by default in the Active Directory Users And Computers console. To view the System container and the Policies subcluster, you can select View | Advanced Features in the Active Directory Users And Computers console.

# Modes of Operation

When Windows 2000 Server is installed on a new computer, it will automatically install as a member server. However, when you are upgrading a Windows NT PDC or BDC, as the Windows 2000 Server installation is complete, Windows 2000 Server will automatically begin the process to install Active Directory by starting the Active Directory Installation Wizard.

An Active Directory has two modes, mixed mode and native mode. When running in mixed mode (the default), one Active Directory server in each domain acts as a PDC for any legacy NT BDCs. This enables backwards compatibility, as well as an incremental upgrade strategy that each server can be migrated and verified before beginning the next. Native mode is required for using Active Directory features such as nested groups and Universal Groups. Native mode cannot be used until all NT BDCs are upgraded, and the domain cannot be returned to native mode after switching.

One of the important differences between native and mixed mode from the system security point of view is that pure Kerberos authentication between domain controllers cannot be used in mixed mode (although the Windows NTLM protocol must also be turned off explicitly in native mode).Another difference is that in mixed mode there is a special group called "Pre-Windows 2000

![](bbox=[0.067, 0.948, 0.295, 0.97])