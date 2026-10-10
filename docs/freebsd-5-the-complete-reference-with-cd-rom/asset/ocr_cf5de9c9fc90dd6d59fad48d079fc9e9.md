best bet is to install several mail clients and try them all. If you're administering a system with many users, you should install a range of mail readers for your users.

> Mail readers don't always use compatible mailbox formats. Thus, you may not be able to easily switch between mail readers and maintain your mail spool. I recommend you create a test account for initial mail reader evaluation.

# Initial Setup and Configuration

After you install a mail application, it should be more-or-less ready to use. There are, however, several details you may want or need to configure. Most of these features are set on a user-by-user basis, generally in configuration files in the user's home directories named after the program. Some programs create an entire subdirectory in which they store these files. Most programs have default configuration files stored in /etc or in the programs' own directory trees. Examples of these files include

+   
+   *   \textbf{pine}	This program stores local defaults in /usr/local/etc/pine.conf. Users can override these defaults in the .pinerc files in their home directories.
+   *   \textbf{Mutr}	The /usr/local/etc/Muttrc file holds global default settings. Users can override these defaults by creating .muttrc files in their home directories.
+   *   \textbf{Skrue}	This program has no global configuration file; instead, it prompts for configuration values the first time it's run, and stores them in ~/. sruce/ sruce.conf.
+   *   \textbf{Sylphed}	Like Sruce, Sylphed prompts for user defaults the first time it's run and stores them in the user's home directory--specifically, in ~/. slyphed/ slyphedrc.
+       

Some programs--particularly the X-based tools, but also some text-mode programs-- enable users to alter their defaults from within the mail program itself. It's generally a good idea to use this feature because it reduces the chance of damaging a configuration with a manual editing error. Figure 24-1 shows an example: the Sruce Configuration Options dialog box. This dialog box appears the first time you launch the program and can be opened again by selecting Settings | Preferences. Most other GUI programs provide a similar dialog box. Options you should be sure to set are

+   
+   *   \textbf{Name and address}	Many programs fill in your name and e-mail address based on information in the FreeBSD account database and default machine information, such as the hostname. You may want to edit this information--say, to remove the host portion of a hostname if your return mail uses only the domain name. Some programs, including Sruce as shown in Figure 24-1, provide a separate option for a Reply-To address. You can use this feature to have replies sent to another address, if recipients' mail programs honor the field.
+       

![](bbox=[0.0, 0.0, 0.0, 0.0])