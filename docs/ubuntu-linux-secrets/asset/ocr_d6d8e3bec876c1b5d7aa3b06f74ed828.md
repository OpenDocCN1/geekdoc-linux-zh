# Part 2: Starting Out with Ubuntu

Ubuntu installs the Bogofilter plug-in as the default system spam filter program for Evolution to help eliminate spam. You can install SpamAssassin as a separate plug-in using the Synaptic Package Manager (see Chapter 13, “Software Installs and Updates”).

> **Secret**
> 
> The Bogofilter Bayesian spam-filtering process works best when it has many data samples to learn from. As spam messages come into your inbox, don’t delete them. Take the extra time to mark those messages as spam by clicking the Junk button in the Evolution toolbar. This step helps expand the Bayesian data model for Bogofilter and block future spam messages.
> 
> Likewise, if Bogofilter should mark any valid messages as junk, you’ll want to click the Not Junk button in the toolbar so that Bogofilter doesn’t make the same mistake on future messages.

# Backing Up Evolution

As you can tell from this chapter, there are plenty of customized settings involved in a well-running Evolution setup. You’ll want to ensure that you have a good backup of your Evolution environment so you don’t have to configure all of those settings again should you lose your Evolution installation.

The easiest way to save your Evolution settings is to use the Backup Settings feature in the File menu. The backup feature creates an archive file that contains the system settings for your Evolution accounts, along with all email messages, contacts, tasks, and appointments you have stored. To create the archive file, Evolution must first be shut down so that it can access all of the files necessary for the backup process. A Notice dialog box appears, asking whether that's all right and whether you want to restart Evolution after the backup completes. Once you create the backup archive file, it’s a good idea to remove it from your system and store it in a safe place, such as on a USB Memory Stick.

If you lose your Evolution settings or data, you can easily restore them by using the Restore Settings feature in the File menu or by selecting the backup archive file in the setup wizard.

# Using the Address Book

The address book in Evolution provides a great place to keep contact information for all your personal and business needs. The Evolution email program can access the address book to add recipients of email messages.

To access the address book, click the Contacts button in the Switcher section of the Evolution window. The main Contacts window appears, shown in Figure 9-13.

The address book window displays a brief entry for each address in the book. If you double-click on an individual entry, the Contact Editor dialog box appears, shown in Figure 9-14.

In the Contact Editor dialog box you can assign names, email addresses, instant messaging accounts, phone numbers, mailing addresses, and other information about the contact. To start a new contact, just click the New button in the toolbar area. A Contact Editor for a new contact appears.