+   * Help
* Compose Message
* Message Index
* Folder List
* Address Book
* Setup
* Quit

Except for Setup and Quit, when you select an item in the preceding line, pine displays a screen for that item. When you select Setup, pine prompts you for a setup task; one you have is Config, which modifies the behavior of pine (refer to “Configuring pine” on page 1282). Selecting Quit returns you to the shell.

Selecting Help in the Main menu displays the Help Main menu, which gives an overview of the pine mailer. This is a good place to start if you are new to pine.

# Sending Messages

Having a pine address book makes sending mail much easier. To set up your address book to add, delete, or edit an entry, select Address Book from the Main menu. For each user you add to your address book, pine prompts you for the user's full name, nickname, and e-mail address. In the Address Book screen, you may also select List to define a distribution list—a group of users you can reference with a single nickname. (A nickname is an alias that easily allows you to remember and reference a recipient or sect of recipients.)

Specifying recipient-list on the command line puts you directly into the Compose screen (see Figure 3-18 on page 90). If you use a full or nickname as an address, pine attempts to map the name to a proper e-mail address (or list of e-addresses), using your address book. If you give a name that is not in your address book, pine assumes the name is a user on your machine. Of course, you can specify any address on the command line; the recipient does not have to be in your address book or on your machine.

You can enter the message composer by selecting Compose from the Main menu. Having access to the Main menu permits you to use other pine functions during your pine session.

The fields for the header of the message are displayed at the top of the Compose screen. If you have included a recipient-list on the command line, To: field is already filled in; otherwise, you need to enter an e-mail address in this field or a full name or nickname as it appears in your address book. Other fields are Cc:, for recipients of “carbon copies” of your message; Attchmnt:, for attaching files