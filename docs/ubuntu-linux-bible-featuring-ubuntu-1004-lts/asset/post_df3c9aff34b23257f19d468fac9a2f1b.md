
The basic steps for reading Gmail using Evolution (or any other mail client) are as follows:

- 1. Configure Gmail to support the mail transport protocol that you want to use.
- 2. Create an account in your mail client that gives you access to your Gmail mail.

The next few sections provide the information that you'll need to do for these steps for both POP and IMAP.

## Selecting a Transport Protocol in Gmail

In order to access Gmail via POP or IMAP, you must first configure your Gmail account to be available via the protocol of your choice. To do this, log in to your Gmail account via Firefox—I mean, via your browser of choice—and select the Settings in the upper-right portion of the section. Next, select the Forwarding and POP/IMAP link in the header of the page that displays. This displays a screen like the one shown in Figure 7-21.

FIGURE 7-21

Configuring Gmail for POP/IMAP

![](img/1a233c34336fbf5a85d6eb785e401709_289_0.png)

## Chapter 7: Managing E-Mail and Personal Information with Evolution

The two bottom settings on this screen enable you to activate POP and IMAP connectivity to your Gmail account. Personally, I tend to favor IMAP over Gmail because that guarantees that all my Gmail mail is archived at Google and enables me to access it from anywhere, including any folders that I set up in my Gmail account. Because I tend to use a variety of systems, this gives me a single view of my mail from anywhere. Your mileage may vary.

### Tip

If you decide that you want to read Gmail via the Web only, you can also activate Forwarding, which will send a copy of any incoming Gmail mail to another e-mail address. To do this, click the “Forward a copy of incoming e-mail to” button, enter your other e-mail address, and make sure that the second configuration list keeps Gmail’s copy in the Inbox. This provides a nice notification mechanism for Gmail, which can be handy if your Gmail account is not your primary e-mail account.

To activate IMAP access to your Gmail account, simply click the “Enable IMAP” radio button and click “Save Changes” at the bottom of the screen.

If you decide to use POP rather than IMAP, a few more configuration choices are available. First, you can either enable POP for all of your mail, or for all of the mail that arrives after the point you configured POP access. Which of these you want depends on how you want to use Gmail:

- If you want to archive all of Gmail correspondence on one of your systems, you will probably want to select “Enable POP for all”. The first time you access your Gmail account with a mail client that is not configured to leave your mail on the server, all of the mail in your Inbox will be downloaded to your desktop system, and what happens to it depends on how you set the “When...
- If you use this option in the hopes of archiving all of Gmail mail on one of your local systems, note that POP only deals with mail in the Inbox. Any mail that you’ve archived in folders that you created in your Gmail account will not be downloaded, only in the Inbox. If your goal is to archive everything locally, you’ll have to copy or move the messages from your folder to your Inbox. Copying them will leave a copy in your Gmail account, but you won’t be able to access those folders via POP.
- If you are simply using your mail client to check your Gmail mail and send messages but have configured your mail client to leave messages on the server, the first time that you check on any new system, you’ll see a delete of all the mail that is still in the Inbox for your Gmail account. In this case, you should probably select the “Enable POP for all mail that arrives from now” radio button.

There are plenty of other scenarios in which you may prefer one option over the other—these are just the most common cases. Personally, I like IMAP.

If you’re still sold on POP, you can use the “When messages are accessed with POP” configuration item to fine-tune what happens to your mail when you read it via POP. These settings are as follows:

- Keep Gmail’s copy in the Inbox: The default setting, this value enables you to read your mail over the Web but still access it via POP. This setting overrides others your mail client wants to delete messages that it has downloaded and can protect you if you forgot to tell your mail client to leave the messages on the server.
- **Delete Gmail's copy:** This value deletes mail from your Gmail Inbox you've read via POP and overrides the settings in your mail client. In other words, even if you've configured your mail client to leave messages on the server, any Gmail mail that you access via POP will be purged from your Gmail account.
- **Archive Gmail's copy:** This value deletes mail from your Gmail Inbox you've read via POP but leaves an archive copy of your Gmail account that you can still access via the "All Mail" link. This also overrides the settings in your mail client. In other words, even if you've configured your mail client to leave messages on the server, any Gmail mail that you access via POP will be purged from your Inbox but will still be available in the "All Mail" link.

When you have activated POP or IMAP on this screen, optionally enable Forward, and specified any configuration parameters, click "Save Changes" at the bottom of the screen. Your configuration changes will be saved, and your Inbox re-displays.

## Part II: Ubuntu Desktop Users

## Accessing Gmail Using POP

To check and read your Gmail via POP, you must specify the following values when creating an account for receiving incoming mail:

- **E-mail Address:** your-username@gmail.com
- **Server Type:** POP
- **Server:** pop.gmail.com
- **Username:** your-username@gmail.com
- **Requires Security/Authentication:** Yes, SSL encryption
- **Port:** 995
- **Password:** your-gmail-password

### Note

**You should, of course, replace your-username and your-gmail-password with the appropriate values for your account when creating a new account in Evolution.**

There are plenty of other configuration options, such as whether you want messages to be stored on the server and for how long, whether you want to automatically check for messages and how often, whether checking mail at this account should be included in a default mail check, and so on. Different mail clients handle this differently. For example, in Evolution, whether you check mail for an account by default depends on whether an e-mail account is enabled in Evolution's main Accounts dialog. You'll probably want to enable this option when first creating and configuring POP access to your Gmail account—you can always disable it after you're sure that everything is working correctly.

## Chapter 7: Managing E-Mail and Personal Information with Evolution

Sending outgoing mail is done via the SMTP protocol. To send access your mail client, you must specify the following values when creating an account for sending:

- **Server Type:** SMTP
- **Server:** smtp.gmail.com
- **Port:** 587 or 465
- **Requires Security/Authentication:** Yes, TLS or STARTTLS. (If this option isn't available, use SSL encryption.)

Test your new account by using an existing e-mail account to send a message, and if you successfully retrieve mail, you should then check that you can send mail using this account. To do this, create a new message using the icon or the File New menu.

To see the official explanation of how to configure POP access to your Gmail account, see https://mail.google.com/support/bin/answer?answer=13287. If you have any problems with the explanation in this section, you may want to check that site, in case something has changed since this post was written.

## Accessing Gmail Using IMAP

To check and read your Gmail via IMAP, you must specify the following values when creating an account for incoming mail:

- **E-mail Address:** your-username@gmail.com
- **Server Type:** IMAP
- **Server:** imap.gmail.com
- **Username:** your-username@gmail.com
- **Requires Security/Authentication:** Yes, SSL encryption
- **Port:** 993
- **Password:** your-gmail-password

### Note

There are always plenty of other configuration options, such as folders to check mail in, whether you want to automatically check for messages and how often, whether checking mail at this account should be enabled in a default mail account and so on. Different mail handle this information differently.
