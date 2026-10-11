
## RESOURCE KIT TOOLS

### DsacIs.exe

The DsacIs.exe (Directory Services Access Control Lists) tool helps you manage access control lists for the Active Directory. When you launch DsacIs.exe, a command prompt opens and displays information about the utility. The purpose of the utility is to display or modify existing Access Control Lists of Active Directory Objects. ACLs determine who can access what Active Directory object. With this command line utility, you can view information about the current ACLs and use the string command to modify ACLs as desired.

When the utility opens, you can see a list of switches and command line codes available to help you manage ACLs. This tool is a useful way to manage ACLs from one location, but you may face a slight learning curve to master the syntax options.

![](img/763d5ae436311371600c0952a3da9094_521_0.png)

![](img/763d5ae436311371600c0952a3da9094_521_1.png)

- Double-click DsacIs.exe in the Resource Kit details pane. The utility opens with a list of syntax and switch options.

### Dsstat.exe

Dsstat.exe (Directory Services Status) is a command-line utility that performs diagnostic tests to detect differences between naming contexts on domain controllers.

For example, you can use Dsstat.exe to compare two different directory trees across different domains. The tool gathers statistical information about the capacity of the domain controllers, such as database size and the number of objects per server. By gathering these statistics, Dsstat.exe can determine if the domain controllers have an accurate image of their own domains.

Dsstat.exe has switches that allow you to refine its operation to specific domains, domain controllers, or global catalogs. It is particularly helpful as a troubleshooting tool.

![](img/763d5ae436311371600c0952a3da9094_522_0.png)

- Double-click Dsstat.exe in the Resource Kit details pane. The utility opens with a list of syntax and switch options.

### Ldp.exe

Ldp.exe is a graphical tool that allows you to perform a variety of LDAP (Lightweight Directory Access Protocol) actions. You can use the tool to connect, bind, and search different servers and gain the LDAP information about different directory objects.

The most important aspect of the Ldp.exe tool is the display of the *metadata*, which is information about the attributes of each object within the directory. You can search for a particular object and gain its full LDAP name, such as CN=CorpServ, CN=Servers, DC=Corp, DC=com. This information is not displayed using a typical LDAP search for an Active Directory object. By using this tool, you can troubleshoot LDAP retrieval problems.

![](img/763d5ae436311371600c0952a3da9094_523_0.png)

1. Double-click Ldp.exe in the Resource Kit details pane. The window opens.
2. Use the menus to connect to different LDAP servers and gather LDAP information.

### Movetree.exe

Movetree.exe is a useful tool for administrators who manage Active Directory environments that are undergoing organizational changes. You can use Movetree.exe to move Active Directory objects and OUs between different domains in a single forest. This utility can be of great value if you find yourself needing to consolidate two domains or move objects and OUs between domains within a forest.

Although Movetree.exe is a useful utility, you should note that the utility does not solve all of the problems with a major resource movement or domain consolidation. Some objects, due to data storage, cannot be moved, and you must perform these moves manually. As always, careful planning to attempt to avert resource movement or domain consolidation is your best action. Yet, in the case of a resource movement or consolidation, this command line utility can be of great value.

![](img/763d5ae436311371600c0952a3da9094_524_0.png)

- Double-click Movetree.exe in the Resource Kit details pane. The utility opens and displays a list of command line switches and options.

## ENFORCING PASSWORD HISTORY

Password history allows the computer to remember passwords that have previously been used on the system. By remembering passwords, the computer can tell a user when he or she is attempting to reuse a password that has previously been used.

You can determine how many passwords you want the policy to remember. The default is only 1, but you can set the system to remember as many as you like. The decision you make depends on the security desires of your organization and whether or not you allow users to reuse old passwords.

![](img/763d5ae436311371600c0952a3da9094_525_0.png)

![](img/763d5ae436311371600c0952a3da9094_525_1.png)

1. **Expand** the Account Policies container and select Password Policy in the left pane. The policy settings appear in the details pane.
2. **Double-click** the Enforce Password History policy setting.
3. **Click** the check box to either enable or disable the policy setting.
4. Use the scroll box to increase or decrease the number of passwords the system remembers.
5. **Click** OK.

## ENFORCING MAXIMUM PASSWORD AGE

Password age is a serious security issue. Most networks do not allow a user to have the same password for an indefinite period of time. The longer passwords are used, the more likely they are to be stolen by unauthorized individuals. A good security plan limits the amount of time a password can be used. The default setting is 42 days. After the time expires, users are prompted to create a new password for their accounts. You can use a shorter or longer time if desired, but create a reasonable length of time. You do not want to force your users to learn—and remember—a new password every week, but you do not want them using the same password for six months—or longer—either.

![](img/763d5ae436311371600c0952a3da9094_526_0.png)

1. Expand the Account Policies container and select Password Policy in the left pane. The policy settings appear in the details pane.
2. Double-click the Maximum Password Age policy setting. The Maximum Password Age window appears. Click the check box to either enable or disable the policy setting.
3. Use the scroll box to increase or decrease the number of days in which the password expires.
4. Click OK.

## ENFORCING MINIMUM PASSWORD AGE

As with enforcing password maximum age, you can also enforce a minimum age. For example, let's say that a particular user is very worried about password security. The user changes his or her password every day, then eventually forgets the password, then the user has to get help. The minimum password age prevents users from changing their passwords too frequently by requiring a certain number of days to pass before they can change their passwords again. By default, the setting is 0 days, which means users can change their passwords any time they desire, but you can change this so that users must keep their passwords for a specified number of days before changing it.

![](img/763d5ae436311371600c0952a3da9094_527_0.png)

1. Expand the Account Policies container and select Password Policy in the left pane. The policy settings appear in the details pane.
2. Double-click the Minimum Password Age policy setting.
3. Click the check box to either enable or disable the policy setting.
4. Use the scroll box to increase or decrease the minimum number of days a password must be used.
5. Click OK.

## ENFORCING MINIMUM PASSWORD LENGTH

For security purposes, you can force users to create passwords that adhere to a certain length of characters. This is a good security policy because longer passwords are more difficult for unauthorized users to steal. As a general rule, a password character length of seven characters should suffice. By setting a length requirement, you prevent users from using simple passwords, such as “cat,” or “dog” or “car,” and so on. The default setting for this policy is 0, which means no length requirement exists, but for good security, you should consider implementing a password length of at least five characters, with seven being your best choice.

![](img/763d5ae436311371600c0952a3da9094_528_0.png)

1. Expand the Account Policies container and select Password Policy in the left pane. The policy settings appear in the details pane.
2. Double-click the Minimum Password Length policy setting.
3. The Minimum Password Length window appears. Click the check box to either enable or disable the policy setting.
4. Use the scroll box to increase or decrease the number of characters the password must contain.
5. Click OK.

![](img/763d5ae436311371600c0952a3da9094_528_1.png)
