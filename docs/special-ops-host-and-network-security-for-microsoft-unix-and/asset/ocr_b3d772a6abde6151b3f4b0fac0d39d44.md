316 Chapter 7 • Securing Exchange and Outlook Web Access

# Mailbox Rights

The actual rights to access a mailbox are little different than the rights for Active Directory objects and the Configuration container data. These rights are assigned to Active Directory security principals (user accounts and security groups), but they are actually saved to the information store where the mailbox is located. The mailbox rights can be viewed through Active Directory Users and Computers, but you must enable advanced features through the View | Advanced Features menu. Figure 7.4 shows the mailbox rights for a mail-enabled user account. You cannot access the mailbox rights information unless the user's information store is mounted and accessible.

# Figure 7.4 Mailbox Rights Assigned and Inherited

![](bbox=[0.328, 0.353, 0.671, 0.603])

Notice that the rights are inherited from the Administrative group or the Exchange organization container. Also note the many SELF in the list of users assigned to the mailbox; this is the Active Directory user account. If you view the mailbox rights list and do not see anyone but the SELF account, this means that the mailbox has not yet been accessed. Once the mailbox has been accessed for the first time, the Active Directory permissions will be inherited.

# Denial of Service and Exchange

Due to the fact that Exchange 2000 is dependent on Windows 2000 and the Active Directory, it goes without saying (yet I'm saying it anyway) that a denial of service attack that causes clients to be denied access to Windows 2000 machines or denies access to the Active Directory will negatively affect Exchange

www.synergy.com