
## Who should be a contact?

Because network user information is stored in the Active Directory, you do not need to create contacts for network users. You can, however, use the contact feature to store information about temporary employees who do not have a network account, consultants, or other business associates who you frequently contact.

## How should contacts be organized?

No hard and fast rules for organizing your contacts exist, but if you want your Active Directory users to easily find the contacts, consider creating an OU that identifies itself as a contact OU, and then storing the contact objects in the OU. Of course, the contact OU can also reside in another OU, depending on your Active Directory structure.

## CONFIGURING A CONTACT

- 1. After you create a contact, choose Action > Properties.
- 2. Use these boxes to enter contact information.
- 3. Use these boxes to enter phone, e-mail, and Web information.
- 4. Use the Other buttons to list additional phone or Web information.

![Image](img/763d5ae436311371600c0952a3da9094_342_0.png)

![Image](img/763d5ae436311371600c0952a3da9094_342_1.png)

## CREATING AND CONFIGURING A CONTACT

**On** the Address tab, enter information in the boxes about the contact's address.

The Telephones tab provides a number of boxes for the contact's phone and pager information. You can enter additional information about contacting the user in the comments section.

On the Organization tab, you can enter information about the contact's organization. If the contact is a member of your organization, you can click the Change button to enter the manager's name from the Active Directory. The Direct Reports box lists the people within your organization who directly report to the contact.

The Member Of tab enables you to add the contact to groups within the Active Directory. Use the Add button to add the selected group(s).

![Image](img/763d5ae436311371600c0952a3da9094_343_0.png)

- 5. Click the Address tab.
- 6. Use these boxes to enter the contact's address information.
- 7. Click the Telephones tab.
- 8. Use these boxes to enter the contact's telephone numbers.
- 9. Click the Other buttons to add additional telephone information.
- 10. Enter any additional comments about the contact.

## TIPS

### Why would a contact have a manager?

Remember that contacts in the Active Directory are loosely defined and can be used in an appropriate manner for your organization. Many organizations hire contractors who directly report to management at the company. These managers are a part of the Active Directory, even though the contractor may not be.

### Should contacts have group access?

Contacts may be considered part of groups as necessary. Without a valid logon and password, however, they cannot use the network or directory resources. Again, the contact can be used in a number of ways, depending on the needs of your organization.

### What is the purpose of the Telephone tab when you can enter the contact’s phone number on the General tab?

The Telephone tab is simply another place to enter additional phone information—such as home phone, pager, cellular phone, and so on—about the contact.

![Image](img/763d5ae436311371600c0952a3da9094_344_0.png)

- **11** Click the Organization tab.
- **12** Enter the contact’s position and company information.
- **13** If the contact has a manager in the local environment, click the Change button to select the manager from the Active Directory.
- **14** Click the Member Of tab.
- **15** If you want the contact to be a member of a group, click Add and select the group.
- **16** Click OK to save your changes.

## USING SHARED FOLDERS

You can publish shared folders in the Active Directory so that users can more easily find information. In the past, a user had to know which server or workstation stored a shared folder. Now, you can store that information in the Active Directory so that users can more easily find shared folders and even search for them. The shared folders and the information they contain still reside on the hosting computer's hard drive, but the directory keeps track of the folder's location so that users don't have to.

With the powerful search features of the Active Directory, a user can perform a search for shared folders, find the folder he or she needs, and simply open the folder from the Active Directory. Knowing the network path to the shared folder is not necessary.

![Image](img/763d5ae436311371600c0952a3da9094_345_0.png)

## ADDING A SHARED FOLDER

- 1. Select the OU in which you want the object to reside and choose Action > New > Shared Folder.
- 2. Use these boxes to enter the shared folder's name and the UNC path.
- 3. Click OK.

### What information can reside in a shared folder?

Virtually any information can reside in a shared folder. Common examples include documents, applications, databases, or other shared folders. Shared folders function the same as they did in Windows NT and contain any shared information. The Active Directory simply provides a directory object for the folder and keeps track of where it is located on the network.

### Where is the information in the shared folder?

The shared folder object in the Active Directory is simply a pointer to a computer that contains the shared folder and the information in the shared folder. The method allows a user to contact a computer, such as CORP64737, and use the shared folder on that computer without having to know that the folder actually resides on CORP64737.

### Does the Active Directory keep track of a shared folder's contents?

No. A shared folder object only provides the pointer to the shared folder and a description of the contents in the shared folder, which an administrator enters.

![Image](img/763d5ae436311371600c0952a3da9094_346_0.png)

![Image](img/763d5ae436311371600c0952a3da9094_346_1.png)

- To perform additional configuration, select the shared folder.
- Choose the Action menu.

## OPENING A SHARED FOLDER

- Choosing Action > Open displays the shared folder and its contents.

## USING SHARED FOLDERS CONTINUED

You can also click Explore in the selection list so that you can see the network directory structure in an Explorer window.

If you click Map Network Drive in the selection list, you can map a network drive to the shared folder that will connect each time you log on. This feature enables you to use My Computer to connect to the share and is a useful feature for shares that you access regularly. The Map Network Drive window enables you to specify a drive letter and shared folder. You can also connect using a different username. This feature is provided for anonymous access and allows administrators to connect to shares as other users. You can also connect to Web folder or FTP site by clicking the link. This opens the Add Network Place Wizard, which allows you to create a connection object on your system. With the ever-growing use of intranet sites, this feature is particularly helpful if you need to connect to a shared folder on the intranet or even the Internet.

![Image](img/763d5ae436311371600c0952a3da9094_347_0.png)

![Image](img/763d5ae436311371600c0952a3da9094_347_1.png)

## EXPLORING A SHARED FOLDER

- Choosing Action → Explore brings up an Explorer window presenting the directory location of the shared folder.

## MAPPING A NETWORK DRIVE TO A SHARED FOLDER

- Choosing Action → Map Network Drive brings up this window.
- Select a drive letter.
- 1. Type the shared folder UNC path.
- 2. Click this link to connect using a different name.
- 3. Click this link to connect to a Web folder or FTP site.

## TIPS

### Why is mapping a drive to a Web folder or FTP site an option?

One of the goals of Windows 2000 is to provide seamless integration with the Internet. You can map a network drive to a Web folder or FTP site on the Internet or intranet just as though the folder were available on your LAN. This feature enables you to access any resource you may need, whether local or not. An important feature of Web folders is user contact over the Internet. A company in several geographic locations can set up a Web site with shared folders available so that network users in other geographic locations can access the information via the Internet. This possibility can reduce site bandwidth by using the Internet.

### Do I need to connect to a shared folder using a different username?

In most cases, no. This option is provided for anonymous access and for users who want to connect using a very secure account (such as an administrator's account).

![Image](img/763d5ae436311371600c0952a3da9094_348_0.png)

![Image](img/763d5ae436311371600c0952a3da9094_348_1.png)

- **4** If you clicked Connect Using A Different User Name, the Connect As dialog box appears.
- **5** Enter the username and password.
- **6** Click OK.
- **7** If you clicked to connect to a Web folder or FTP site, the Add Network Place Wizard appears.
- **8** Type the location information or click Browse.
- **9** Click here to see some examples of shared folder, Web folder, and FTP site syntax.
- **9** Click Next to continue, and then click Finish.

CONTINUE
