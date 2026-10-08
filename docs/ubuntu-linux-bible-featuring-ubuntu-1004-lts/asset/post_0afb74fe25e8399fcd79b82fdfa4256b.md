
# Chapter 7: Managing E-Mail and Personal Information with Evolution

## Search Folders

- Right-click on the heading on any sample message that satisfies the criteria for the search folder that you want to create, select the "Create Rule From Message" submenu, and select any of "Search Folder from Subject," "Search Folder from Sender," "Search Folder from Recipients," or "Search Folder from Mailing List." (The last displays only if you select a message that Evolution can recognize as having been sent to a mailing list). Each of these menu commands creates an initial search folder based on the specified portion of that mail, which you can retain or further customize.
- Select the Edit menu's "Search Folders" command and click Add to create a new search folder.
- While any sample message that satisfies the criteria for the search folder that you want to create is highlighted, select the Message menu's "Create Rule" and select any "Search Folder from Subject," "Search Folder from Sender," "Search Folder from Recipients," or "Search Folder from Mailing List." (The last displays only if you select a message that Evolution can recognize as having been sent to a mailing list). Each of these menu commands creates an initial search folder based on the specified portion of that mail, which you can retain or further customize.

Performing any of these actions displays a dialog like the one shown in Figure 7-18 that contains any criteria implied by the command you selected.

![](img/1a23c34336fbf5a85d6eb785e401709_282_0)

## Filters

Once this dialog displays, you can specify a name for the search folder and refine the criteria for the search folder in the same way you create filter rules for incoming mail, explained in the next section. The primary difference between search folder and filter rule lies in the bottom half of the dialog shown in Figures 7-18 and 7-19, which (for search folders) identifies the location(s) that the folder should search. You can specify that only certain folders are searched by clicking Add and selecting their names, or you can select "All local folders" or "All remote folders" to search the server. Figure 7-19 shows a search folder that has been defined to search only a specific set of local folders.

### FIGURE 7-19: A search folder associated with local folders

![](img/1a23c34336fbf5a85d6eb785e401709_283_0)

Once you are finished fine-tuning the rule that messages must match to be included in your new search folder, click OK to close this dialog and return to Evolution. The search folder is under the Search Folder item in Evolution's navigation pane and contains existing messages that matched the criteria.

## Filtering Incoming Mail

We receive a significant amount of e-mail, some of which we actually want to receive. A fact of modern life is that all of us receive a significant amount of spam or junk mail—essentially mail we didn't ask for but is either broadcast to randomly generated addresses or perhaps sent to us directly.

Evolution provides two sophisticated features for automatically analyzing incoming mail and performing specific actions on mail messages that match these criteria. In the case of legitimate mail, Evolution enables you to create powerful filtering rules that can automatically filter incoming mail into appropriate folders. Mail filters can also discard incoming messages from known spam sites, messages that contain words only a spammer would use, or messages that match any other criteria that you define.

In addition to making it easy for you to create powerful filtering rules, Evolution can also be integrated with other free Linux software that uses different approaches to inspect spam and junk mail and automatically move it to your junk folder. You can then quickly scan your junk folder occasionally to see if all the mail there is indeed junk, and if so, you can easily delete it without having to read.

The next two sections explain how to create your own filter rules and how to install the software required for junk mail processing in Evolution on Ubuntu.

## Automatically Processing Incoming Mail

To expand on the definition of filtering given in the introduction to this section, filtering e-mail means to analyze its contents based on various criteria and to use the results of examination to perform some action regarding that message. Message filters are typically applied to incoming messages that are stored locally—or a remote server (if your Inbox is on an IMAP server, you must specify that as an option when creating your account, as shown in Figures 7-6 and 7-7).

As with most tasks in Evolution, there are several ways to create a new mail filter. These include the following:

- Right-click on the heading of any sample message that satisfies the criteria for the filter you want to create, select the "Create Rule From Message" submenu, select "Filter on Subject," "Filter on Sender," "Filter on Recipients," or "Filter on Mailing List." (The last displays only if you select a message that Evolution can recognize as having been sent to a mailing list.) Each of these menu commands creates an initial message filter based on the specified portion of that mail message, which you can retain as is further customize.
- Select the Edit menu's "Message Filters" command and click Add to create a new message filter.
- While any sample message satisfies the criteria for the filter that you want to be highlighted, select the menu's "Create Rule" submenu and select any "Filter on Subject," "Filter on Sender," "Filter on Recipients," or "Filter on Mailing List." (The last displays only if you select a message that Evolution can recognize as having been sent to a mailing list.)

Performing any of these actions displays a dialog like the one shown in Figure 7-20 that contains any criteria implied by the command you selected.

### FIGURE 7-20: Creating or editing a message filter

![](img/1a23c34336fbf5a85d6eb785e401709_285_0)

When creating a message filter, the default action to perform on matching messages is to move that message to a specified folder. To identify that folder, click "select a folder" and locate the target folder in the navigation dialog that displays.

Evolution provides a very sophisticated set of possible ways of matching messages in message filter. The following are the portions of the message that you can match and the comparison operators that you can use. These correspond to the contents of the dropdown menus you see when clicking on the first two buttons when creating or editing a rule:

- You can examine the following portions of a mail message when creating a rule: Attachments, Data Received, Date Sent, Expression, Flow, Junk Test, Label, Match All, Message Body, Mailing List, Pipe to Program, Recipients, Regex Match, Score, Sender, Size (KB), Account Size, Specific Header, and Subject.
- You can analyze those portions of an e-mail message using the following operators: Contains, Does Not Contain, Does Not End, Does Not Sound, Does Not Start With, Ends With, Is After, Is Before, Is Greater Than, Is Less Than, Is Not, Returns Greater Than, Starts With, and Sounds With. Some of these operators can only be used when examining specific portions of a mail message. For example, the "Is After" and "Is Before" can only be used with dates.
