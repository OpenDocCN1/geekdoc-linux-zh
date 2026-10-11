# UNINSTALLING
THE ACTIVE DIRECTORY

You can choose to uninstall the Active Directory from a domain controller, but after you perform this action, the domain controller is demoted to a member server. Every domain controller must have the Active Directory installed.

From time to time, you may have reason to uninstall the Active Directory and demote your server.

As hardware needs change and as your server becomes outdated, you can demote it and use it as a member server, a print server, or an application server. Older machines can perform these tasks effectively without having to run the intensive overhead of the Active Directory.

To uninstall the Active Directory, you use a command-line tool called

dcpromo.exe. You can use dcpromo.exe to upgrade a server to the Active Directory or remove the Active Directory. The Configure Your Server tool does not provide you with a way to demote the domain controller, but it does give you the instructions for using dcpromo.exe.

![](bbox=[0.03, 0.55, 0.49, 0.88])

+   1. Choose Start\[icon\]Run.

![](bbox=[0.52, 0.55, 0.97, 0.88])

+   ■ The Run window appears.