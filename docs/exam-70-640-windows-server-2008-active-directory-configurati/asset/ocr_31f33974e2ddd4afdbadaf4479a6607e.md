After completing this lesson, you will understand the benefits and overall architecture of Group Policy Objects (GPOs). You will be able to describe the Group Policy Container and Group Policy Templates, as well as the use of the Group Policy Management Console (GPMC). You will be able to configure Group Policy settings, understand how GPOs are processed, and fine-tune the application of GPOs.

# Introducing Group Policy

> THE BOTTOM LINE
> 
> Group Policy is a method of controlling settings across your network. Group Policy consists of user and computer settings on the Windows Server 2008, Windows Server 2003 family, Microsoft Windows 2000 family, Window Vista, and Microsoft Windows XP Professional platforms that can be implemented during computer startup and shutdown and user logon and logoff. You can configure one or more GPOs within a domain and then use a process called *linking*, which applies these settings to various containers within Active Directory. You can link multiple GPOs to a single container or link one GPO to multiple containers throughout the Active Directory structure.

The following managed settings can be defined or changed through Group Policies:

+   *   *Registry-based policies*, such as user desktop settings and environment variables, provide a consistent, secure, manageable environment that addresses the users’ needs and the organization’s administrative goals. As the name implies, these settings modify the Windows Registry.
+   *   *Software installation policies* can be used to ensure that users always have the latest versions of applications. If application files are inadvertently deleted, repairs are made without user intervention.
+   *   *Folder redirection* allows files to be redirected to a network drive for backup and makes them accessible from anywhere on the network.
+   *   *Offline file storage* works with folder redirection to provide the ability to cache files locally. This allows files to be available even when the network is inaccessible.
+   *   *Scripts* including logon, logoff, startup, and shutdown scripts, can assist in configuring the user environment.
+   *   *Windows Deployment Services (WDS)* assists in rebuilding or deploying workstations quickly and efficiently in an enterprise environment.
+   *   Microsoft Internet Explorer settings provide quick links and bookmarks for user accessibility, in addition to browser options such as proxy use, acceptance of cookies, and caching options.
+   *   Security settings protect resources on computers in the enterprise.

Depending on the organization’s needs, you can choose which features and settings you wish to implement. For example, you may need to create a policy for a public access computer in a library that configures the desktop environment with a proprietary library-access system. In addition, you might wish to disable the ability to write to the computer’s hard drive. As you determine the needs of different users and address those needs within corporate security and computing policies, you can plan the best methods to implement Group Policy.

Although the name *Group Policy Object* implies that policies are linked directly to groups, this is not the case. Group Policies can be linked to sites, domains, or OUs to apply those settings to all users and computers within these Active Directory containers. However, an advanced technique, called *security group filtering*, will allow you to apply GPO settings