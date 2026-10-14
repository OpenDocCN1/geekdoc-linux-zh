
# Figure 9.17
Exchange Server
Options window.

![](img/415c89a1ede71e11e5040a0038b6916c_405_0.png)

- 2. Select your site and then select Options from the Tools menu. You will see the window in Figure 9.17.
- 3. Make any changes to the naming option that you desire and then click OK. The changes will take effect immediately.

Your Exchange server is almost ready for action. All that is needed now are mailboxes, and if you desire, distribution lists. These are discussed in the next few sections.

## CREATING MAILBOXES

Obviously, everything we have done up to now would be pointless if we didn't create some mailboxes for your users. Each mailbox is assigned to a user on your domain and stores all of that user's Exchange Server data. The mailboxes are contained in the Exchange Server's private information store. Only the user assigned to the mailbox can access the information contained in the mailbox. The steps below describe how to create a mailbox in Exchange Server:

- 1. Open the Exchange Server Administrator from the Microsoft Exchange Start menu program group. You will see a window similar to the one in Figure 9.12.

# Figure 9.18

New mailbox Properties window.

![](img/415c89a1ede71e11e5040a0038b6916c_406_0.png)

- 2. Expand your site, and then select the Recipients container at the bottom of the list.
- 3. Select New Mailbox from the File menu and the new mailbox Properties window in Figure 9.18 will be displayed.
- 4. Complete the First name and Last name fields and the Display and Alias fields will be completed automatically.
- 5. Click the Primary Windows NT Account button to assign an account to the new mailbox. You will be given the choice of choosing an existing account or creating a new account. Choose the option you desire to assign the new account to the mailbox.
- 6. Click OK to create the new mailbox.

At this point, the new mailbox is ready for use. However, you may have noticed that there were many options available in the mailbox Properties window that we did not configure. Table 9.6 describes the different options available in the mailbox Properties window.

| Table 9.6 Mailbox Properties Window Options. |
| Tab Name | Description |
|---|---|
| General | Allows configuration of the user's name, address, office information, and Windows NT account information. |
| Organization | Allows you to configure the user's place in the organization, such as who he/she reports to and other users who are subordinates. |
| Phone/Notes | Allows you to specify additional phone numbers and make notes about the user or mailbox. |
| Distribution Lists | Allows you to view and modify the user's membership in distribution lists. |
| E-mail Addresses | Allows you to add, remove, and edit the email addresses assigned to the mailbox. The Exchange server will accept only mail sent to known email addresses. |
| Delivery Restrictions | Allows you to specify recipients who can and cannot send/receive mail to/from the current user. |
| Delivery Options | Allows you to configure options for users who can send mail on behalf of the current user, and to configure an alternate recipient. |
| Protocols | Allows you to customize Exchange Server protocols for the current mailbox. You should not have to modify the default settings. |
| Custom Attributes | Allows you to configure site-specific custom attributes for message tracking purposes. |
| Limits | Allows you to configure information store usage limits and message size restrictions. |
| Advanced | Allows you to customize some mailbox features. This option is rarely modified. |

## CREATING DISTRIBUTION LISTS

Distribution lists are Exchange Server's version of mailing lists. You can use distribution lists to send messages to multiple mailboxes using a single Exchange alias. Distribution lists can be stored in the recipients container, but for organizational purposes, it is desirable to create a separate recipients container for your distribution lists. This section will detail the procedures, for how to create a new recipients container for your distribution lists, and how to create a distribution list in the new container.

### Creating a New Recipients Container

Use the procedure below to create a new recipients container:

- 1. Open the Exchange Server Administrator from the Microsoft Exchange Start menu program group You will see a window similar to the one in Figure 9.12.
- 2. Select your site and then choose New Other and then Recipients Container from the File menu. The Distribution Lists Properties window in Figure 9.19 will appear.

Figure 9.19
Distribution Lists Properties window.

![](img/415c89a1ede71e11e5040a0038b6916c_408_0.png)
