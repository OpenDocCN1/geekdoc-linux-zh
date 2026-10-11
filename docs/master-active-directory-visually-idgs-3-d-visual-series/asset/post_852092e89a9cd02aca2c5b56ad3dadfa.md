
## Can Active Directory users make changes to group membership?

No. You must have appropriate permissions to be able to change group membership. The interface provided for users allows them only to view the group members—they cannot access properties sheets for the group object or use the Add button without appropriate permissions.

## Besides browsing the directory, is there another way to find a group?

Yes. As with any Active Directory object, you can perform an LDAP search. For example, if you wanted to find the Management group, you can access a search window and run a search for Management. The Active Directory returns the matches, and then you can access the members list of the Management group.

![](img/763d5ae436311371600c0952a3da9094_328_0.png)

2 Double-click the group icon that you want to view.

![](img/763d5ae436311371600c0952a3da9094_328_1.png)

The group members and a description of the group appear.

![](img/763d5ae436311371600c0952a3da9094_328_2.png)

## CREATING A NEW COMPUTER ACCOUNT

Just as a domain user has a user account that represents that person, a computer account represents an actual computer on the network. Each Windows 2000 and Windows NT computer in a Windows 2000 network has a computer account in the Active Directory. Windows 9x computers do not have the security features of Windows 2000 and Windows NT, and therefore do not have computer accounts, but they can still log on to the domain and access resources.

You can also manually add a computer account to the Active Directory, and the process for adding a computer account is very similar to adding a user or group. By adding computer accounts to the Active Directory, you can identify computers on the network that do not automatically have a computer account configured for them (Windows 2000 and Windows NT). Windows 2000 and Windows NT computers must have computer accounts in the Active Directory in order for them to actively participate in the domain.

![](img/763d5ae436311371600c0952a3da9094_329_0.png)

- 1 Select the Computers OU (or another OU in which you want to store the computer account).
- 2 Choose Action->New->Computer.
- 3 Type the name of the computer.
- 4 Click Change if you want to change the group that can join the computer to the domain.
- 5 Select the desired group or user.
- 6 Click OK.
- 7 Click OK to close the New Object - Computer window.

![](img/763d5ae436311371600c0952a3da9094_330_1.png)

- 8 The new computer account appears in the details pane.

## TIPS

### How can I use computer accounts?

Just as you can organize users into a group to assign permissions, you can organize physical computers into groups to assign permissions. For example, if you want only a particular set of computers to use a certain printer, you can assign permissions for that group of computers. This way, no matter what user is logged on to the computer, that user can access the printer for that group.

### How can I create a computer account for a Windows 98 computer?

Only Windows 2000 and Windows NT computers can have accounts in the Active Directory. This is due to the lack of advanced security features in the Windows 9x generation. Windows 9x computers can, however, log on to a Windows 2000 server and participate on the network.

### Can previous versions of Windows use a computer account I create?

Yes. When you create the computer account, click the Allow Pre-Windows 2000 Computers To Use This Account check box to enable this feature.

![](img/763d5ae436311371600c0952a3da9094_330_0.png)

## CONFIGURING COMPUTER ACCOUNT PROPERTIES

Just like users and groups, computer accounts have Properties sheets. You can configure computer accounts by accessing the properties sheet. To access the properties sheet, select the computer account, access the Action menu, and click Properties.

Configuring computer accounts is rather easy. Of particular interest on the General tab, you can choose to click the Trust Computer For Delegation check box. Just as you can delegate duties to user accounts, you can also delegate duties to computer accounts. This feature does require careful consideration so that you do not create security breaches with computers operated by nonadministrative personnel.

The Operating System tab simply displays OS version and service pack information about the computer, and as with other properties sheets, the Member Of tab allows you to configure the computer account's group memberships.

![](img/763d5ae436311371600c0952a3da9094_331_0.png)

- 1. To access the properties sheet, select the computer you want to administer.
- 2. Choose Action→ Properties.
- 3. Type a description in this box if desired.
- 4. Click this check box if you want the computer to be trusted for delegation.

![](img/763d5ae436311371600c0952a3da9094_332_0.png)

### To how many groups should a computer belong?

In order to manage access permissions and keep your network organization from becoming confusing, assign computers only to groups that they absolutely need to belong. Also, remember that after a user logs on to that computer, the user effectively has membership to the groups that the computer is assigned. As with group accounts for users, planning is of utmost importance.

![](img/763d5ae436311371600c0952a3da9094_332_1.png)

### What is the down-level name?

In Windows 2000, all earlier versions of Windows, such as NT and 9x, are called *down-level computers*. Down-level computers used NetBIOS to establish a friendly name, such as Server12. In Windows 2000, DNS is used for name resolution, so in mixed environments, both the DNS and the NetBIOS name are often displayed for objects.

![](img/763d5ae436311371600c0952a3da9094_332_2.png)

5 Click the Operating System tab.

This tab displays the computer's operating system, version number, and the service pack that is applied (if any).

![](img/763d5ae436311371600c0952a3da9094_332_3.png)

6 Click the Member Of tab.

This tab tells you what groups the computer currently belongs to.

7 Click Add to add the computer to more groups.

- 8 Select a new group from the list.
- 9 Click Add.
- 10 Repeat Steps 8 and 9 to add additional groups as needed.
- 11 Click OK when you are done.

The new group(s) appear on the Member Of tab.

## CONFIGURING COMPUTER ACCOUNT PROPERTIES

The Location and Managed By tabs provide the same configuration options as other properties sheets. The Location tab tells which locations are served by the site in the directory setup. You can use the Browse button to change site locations if necessary.

The Managed By tab allows you to enter a manager for the computer account. When you enter a manager, the manager's contact information (such as telephone, address, and so on) is extracted from the manager's user account and placed on this tab, if the information is available in the user account. You do not have to assign a manager to a computer account, but the Active Directory provides you this option so you can decentralize administrative duties in your network. Like delegation, you can assign managers to various Active Directory objects to remove the management burden from senior IT administrators.

![](img/763d5ae436311371600c0952a3da9094_333_0.png)

![](img/763d5ae436311371600c0952a3da9094_333_1.png)

### Who should manage a computer account?

Any number of domain users can be the manager of a computer account. You should select someone who works primarily with the physical computer or manages a group of computers and employees. Remember that group memberships should be carefully configured, so the manager needs to understand the dynamics of group membership and group management. Also, you should minimize the number of people who manage Active Directory objects, for security purposes as well as administrative control.

### Should a computer account belong to different groups?

You can give a computer account membership in any group, just as you can a user account. The group memberships define what actions that particular computer can perform and how that computer can be used on the network. The rule of thumb is to give group memberships that are necessary, but do not assign excessive memberships to either users or computers.

![](img/763d5ae436311371600c0952a3da9094_334_0.png)

12 Click the Location tab.
The Location tab tells you which locations are served by the site.

13 For multiple sites, you can use the Browse button to browse to a different location.

![](img/763d5ae436311371600c0952a3da9094_334_1.png)

14 Click the Managed By tab.
The Managed By tab gives you the name and contact information for the account manager.

15 Use Change to change the computer account manager.

16 Click OK to close the Properties sheet.
