
![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_192_0.png)

Figure 12. Use the Receiving Mail tab to configure the server for incoming mail.

The Server Type is most likely POP unless you know you're using an IMAP server. The Host can be one of two types of values. It might be an IP address as shown in Figure 12, or it might be a fully qualified domain name. If you're using a third-party ISP, your e-mail host name might be a string like “mail.pop3.pacbell.net,” or something similar.

Finally, the Username is the name with which you log on to your mail server. It's not your e-mail address, but in some cases the first part of your e-mail address and your account name might be the same. If you're using a third-party ISP mail account, it's the account name they've given you. When you attempt to connect the first time, you'll be prompted for the password that goes with this account name.

You can skip the third tab, Receiving Options, as shown in Figure 13, but it has useful options for handling your mail.

Some people like incessant interruptions during the day, and so check the “Automatically check for new mail every N minutes” check box. If you travel a lot and use multiple computers, you may also want to check the “Leave messages on server” check box. That way, you can download to your notebook copies of messages while you're on the road and leave the originals on the mail server, and then when you get back to the office (or home), you can download them again, deal with the unread messages, and then have the client on your desktop delete them.

Unless you're terribly shy, you'll probably want to send mail as well as receive it. Use the fourth tab, Sending Mail, as shown in Figure 14, to configure the server that you connect to in order to send mail.

There are just two critical fields in this tab: Server Type and Host. Server Type is ordinarily going to be SMTP unless you know specifically that it's different. The Host field should be filled in similarly to the Host field on the Receiving Mail tab. It may have different specific values, though, because some organizations use different e-mail servers to handle incoming and outgoing e-mail, in order to spread out the load.

For example, the Receiving Mail IP address might be 192.168.2.1 and the Sending Mail IP address might be 192.168.2.2, or they might be “mail.pop3.pacbell.net” and “mail.smtp.pacbell.net”. Again, the settings from your old Windows machine will help you.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_193_0.png)

Figure 13. Use the Receiving Options tab to configure incoming mail.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_193_1.png)

Figure 14. Use the Sending Mail tab to configure outbound e-mail.

## Using Evolution

Although Evo is a multipurpose application, I’m just going to cover its basic e-mail functions: sending and receiving.

Sending e-mail is simply a matter of clicking the New button, filling in the To and Subject fields, typing a note, and clicking the Send button. If you’ve created multiple accounts, you can choose which account to use by clicking the From combo, shown in Figure 15.

Receiving e-mail is just as simple. Click the Send/Receive button, and messages queued up on the incoming mail server will be brought to the in-box. You can create filters to act on incoming mail and perform the actions you specify. Click Tools | Filters to open the Filters dialog, and then click Add to use the Add Rule dialog, shown in Figure 16.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_194_0.png)

Figure 15. You can choose to send a message from multiple Evo accounts.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_194_1.png)

Figure 16. You can create custom rules to handle incoming or outgoing e-mail.

You'll see that you can create a wide variety of rules that include one or more conditions. The conditions are evaluated against the message, and then one or more actions are executed if the conditions are met. In Figure 16, the incoming condition checks for the string “Linux ThinkPad” in the subject line; if it’s found, the message moves to the LTP folder.

Sometimes it can be a pain to create a message condition from scratch; you can create filters based on information in the currently selected message, as shown in **Figure 17**.

Right-click an individual message, select Create Rule From Message, and then select one of the “Filter on” menu items. If the message is from a mailing list, there will be a special menu item to handle it.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_195_0.png)

Figure 17. You can create filters based on a specific message.

## KMail

KMail is KDE’s default graphical e-mail client. Unlike Evolution, KMail does one thing—handle e-mail—and does it well.

### KMail setup

KMail has the same three-pane interface as Evolution and other graphical e-mail clients, but as with Evolution, it doesn’t do you much good until you set it up. Click Settings | Configure KMail to open the Configure dialog, shown in **Figure 18**.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_196_0.png)

**Figure 18. Use the Configure dialog to set up preferences for using KMail.**

The interface is similar to that of Evolution, with icons on the left that drive the appearance of various screens in the dialog, and a list box in the middle that displays the e-mail accounts. Click New to create a new account, or highlight an existing account and click Modify to change its attributes. The Rename button simply allows you to edit the value in the Identity Name column.

The first account that you create automatically becomes the default mail account; once you have multiple accounts, you can make another account the default by highlighting it and clicking the Set as Default button on the right side of the dialog.

The Edit Identity dialog provides tabs for basic and advanced features, as shown in **Figures 19 and 20**. You have to fill in values for the “Your name” and “Email address” fields, pursuant to the same suggestions made for Evolution in the previous section.

The Advanced tab, shown in **Figure 20**, allows you to set some of the same options as in the various optional tabs in Evolution’s setup dialog.

You'll notice that there aren't any places for incoming and outgoing server settings in the Edit Identity dialog. Rather, you need to select the Network icon on the left and then work with the items in the list box and the command buttons on the right as shown in Figure 21. You'll see that you can edit common options under the list box. Selecting the highlighted account and clicking the Modify button will open the Modify Transport dialog, as shown in Figure 22.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_197_0.png)

*Figure 19. You have to fill in a name and e-mail address on the General tab before sending e-mail.*

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_197_1.png)

*Figure 20. The Advanced tab allows you to specify automatic addresses and default folders.*

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_198_0.png)

**Figure 21.** The Network tab of the Configure dialog allows you to control the settings of the incoming and outgoing mail servers.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_198_1.png)

**Figure 22.** The Modify Transport dialog for the incoming e-mail server.

At a minimum, you'll need to enter values for Host and Port. The Host value is the same as described in the configuration section for Evolution—either an IP address or a domain name. The default Port number is 25, but you can change it to suit your specific circumstances.

Clicking the Receiving tab in Figure 21, selecting an account, and then clicking Modify will open the Modify Account dialog for fetching e-mail, as shown in **Figure 23**.

You'll have to supply values for the Login, Password, and Host fields at a minimum, just as for Evolution. And as in **Figure 22**, you can change the Port number if you need to. There are a number of handy settings in this dialog as well. For example, the `Exclude from 'Check Mail'` check box removes this account from the automatic retrieval of mail—handy when you want to retrieve mail manually from an account.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_199_0.png)

Figure 23. The Modify Account dialog for incoming e-mail.

### Using KMail

KMail is just as easy to use as other graphical clients. To send a message, click the New Message icon in the toolbar, or select Message `New Message'. Fill in the From, To, and Subject values in the Composer dialog, and then type the message body.

A particularly nice feature of KMail is that it allows you to select e-mail addresses from a list of recently used addresses, even if they're not in your address book. For example, I removed all of the e-mail addresses in my address book and then clicked the ellipsis (the button with the three dots to the right of the To: text box) to open an empty Addressbook dialog, shown in **Figure 24**.
