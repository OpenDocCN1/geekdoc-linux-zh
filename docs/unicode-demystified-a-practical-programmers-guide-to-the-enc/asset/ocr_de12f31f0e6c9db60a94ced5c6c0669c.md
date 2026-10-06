The recipient-list may contain e-mail addresses, user names (for users on your system), or nicknames that you establish when setting up your address book. You may also use a nickname to refer to a set of addresses.

# # Options

+   - -conf Sends information about the current configuration to standard output.

+   - -feature-list=[no-]|feature-list-option. For example, including -feature-list=enable-flag-cmd on the command line provides you with a Message Index menu item that changes the status flags. Prepending no- to the feature-list-option unsets the option. Refer to “Configuring pine” on page 1282 for a discussion of feature-list-options

+   - folder Opens the opener by folder. Without this option opens the INBOX folder.

+   - i Enters the Message Index directly to read your mail.

+   - -variable=variable-value Assigns the value variable-value to the named variable variable. This option overrides the value given in /etc/pine.conf file in your home directory. For example, giving the option -signature-file=/.fusig pine to insert the contents of the ~/.fusig file in each message you send.

+   - -sort-type=[reverse] Sorts messages. By default the message headers displayed in the Message Index screen are sorted by arrival time. You can have pine sort on a different field by giving the -sort option on the command line. The argument sort-type identifies the sort field. In addition to arrival, you can specify subject, from, date, and size. To reverse the order of the sort, append /reverse to the sort-type.

+   - -h Displays a list of options that you can use with the pine command, along with a summary of each command.

# # Discussion

At the top of all pine screens is a status line that includes the name of the current screen and other status information. At the bottom of each pine screen is a two-line menu of commands that are defined for that screen. If there are too many commands to fit in two lines, pine displays a command that you cycle through two or more partial menus.

Every pine screen allows you to use an aspect of pine’s functionality. Help is available when you need to make decisions.

The following items appear in the Main menu (see Figure 3-17 on page 89):