
# 764 Part V SUSE Linux in the Enterprise

As we have already created a group of users, we can tell SLOX that just those users to have access to this folder.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_808_0.png)

Figure 30-24: Setting the access controls on a shared folder

- 4. Either select a group that you want to give access to, or use the filter to select specific users.

With the ACLs in the Cyrus IMAP server, you need to set the access control on the folder. We trust our architects, so we have given them full access to the folder. To change your ACLs, click Set. The ACLs are implemented immediately.

# Checking System Resources

If you want to monitor the health of your SLOX system, you can either log directly to the folder, or use the web interface to get an overview of running services, system load, and the status of the mail queue.

Click in the Monitor section and select the component of the system you want to view. The System Statistics view, in Figure 30-25, will give you a history of the system load, free memory, and the CPU usage of the SLOX server. This can help when you monitor how well your hardware is coping with the load and see peaks in the mail server for your busiest times.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_809_0.png)

**Figure 30-25:** Viewing the system load

You can view the performance statistics of the SLOX server over a period of time if you want (for example, the last month) or narrow it down to one day. These are good statistics to when asking management for more hardware!

# The User Perspective

When you configured SLOX to your network and add your users, they can start using the functionality of SLOX through the web interface or the i/OSLX connectors. To log in as a normal user, go to the URL for your SLOX installation and enter the credentials of the user you want to log in.

When you initially log in SLOX as a normal user, you are presented with an overview of groupware for the day (see Figure 30-26). This is very much the same as the Outlook today screen.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_810_0.png)

# Reading Your Mail

To view your mail through the web interface, select the eMail from the list of icons across the Portal screen. You will be presented with an easy-to-use email client that you should be familiar with if you have used any of the popular web services (Figure 30-27).

On the left side of the screen is a list of the folders that you have through IMAP. If you created an IMAP account on your desktop email client, these are visible as any normal folder on the right.

Notice in the Inbox that we have a new email that was generated when we created the SolutionsArchive folder in the chapter. When you select an email from the top pane, it is displayed in the lower window, just as it is with the preview pane of most clients.

If you need to send a message, you can simply select the New Message option in the top-left section of the screen. A New message screen displays, as shown in Figure 30-28, and you can compose an email to send just as you do in any email client.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_811_0.png)

Figure 30-27: The email client

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_811_1.png)

Figure 30-28: Sending an email with the web client

# The Calendar

Any changes you make to your calendar through the web interface will be replicated to your Outlook calendar the next time. This is also true for other sections that map onto the Outlook functionality. To add a new calendar entry, follow these steps:

- 1. Select the Calendar section and click the icon that looks like a star. A screen similar to the one shown in Figure 30-29 is displayed.
- 2. As with most calendar applications, you can select begin and end times for the entry, choose to make this entry an all-day event, select what date you want to create it on, and also set a reminder for the entry. When you are happy with the calendar entry, click Save.
- 3. When the entry has been created, you can select that day on the right side of the screen to see what your calendar looks like for that day.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_812_0.png)

Figure 30-29: Creating a new calendar

# Jobs (tasks)

The task list is actually in SLOX. Many of our customers have found it annoying that there is a difference in name between Outlook and SLOX. To create a new job, follow these steps:

- 1. Select the Jobs section and click the new icon (the star!). A screen similar to the one shown in Figure 30-30 is displayed.
- 2. With the new task, you can select the amount, due date, and cost associated with the task itself. This is a kind of project definition and not just that you may be used. To commit the new task to the system, click the Save button.
- 3. When a task has been created, you can create it in the task list along with millions of other things you probably have to do in one day (we all know there aren't enough hours in the day, right?) by clicking the Jobs section in the main menu.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_813_0.png)

Figure 30-30: Creating a new task

# Creating Documents

SLOX has the capability to manage your documents and versioning for those documents through the Documents section of its interface (see Figure 30-31). It is not the most ideal document management system in the world, but it serves its purpose.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_814_0.png)

When you create a document, you can set a description and an ACL for the file (by clicking Read access or Write access) so that other users can access it. When you have set the description on a file, the File save tab to actually upload the file you want to version (see Figure 30-32). When the file has been uploaded, SLOX sets the size and MIME type automatically as well as the filename that users will see when they browse the document tree.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_815_0.png)

Figure 30-32: Uploading a new file

When you have saved the file, you can view its details in the document tree by hovering your mouse over the entry.

When you upload a file, its details are stored in the database, but the file itself is referenced on the filesystem of the SLOX installation. The file will be saved under /var/opt/config/freespool. If you are heavily using the document system, it is advisable to store the /var/opt/config/freespool directory on a separate rated partition or SAN partition.

# Creating a Note

In SLOX, entries are Pinboard entries. A note is just a small sticky note for you to remind yourself of something that can be displayed on your portal screen when you log in to SLOX as a normal user. Again, these Pinboard entries are not elegant as some people would like, but they do the purpose they have been designed to fulfill.

To create a Pinboard entry, click the Pinboard section and the new icon (yes, the star). You can create your note in the screen shown in Figure 30-33.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_816_0.png)

Figure 30-33: Creating a note

To save the note, click Save. The note will then be viewable from the Portal page.

# Creating a New Contact

A SLO user has two address books, private and public:

- The private address book should be used to store personal contacts, or those contacts that are not relevant to running the business.
- The public address book contains all SLOX users' details and also any contacts that you save as. You can write to the public address book only if the administrator gave you write access when your account was created or has given you access after your account was created.

To access contacts, you select the Contacts section. Clicking the new (star) icon will present you with a new contact form. It is quite through in the information you can store about the person or organization you want to add an address for Figure 30-34.

When you are happy with the contact information, click the Save button to insert the entry into the LDAP server.
