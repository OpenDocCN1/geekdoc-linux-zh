+   Ko     Saves the attachment to a file.  
+   K v     Views the attachment.  
+   K I     Pipes the attachment to another program.  
+   WM v     Views all the attachments in the current message.

These commands accept a numeric prefix. For example, you can type

2 Ko

This saves the second attachment to a file.

# ## Mail without News

You probably don't want to open a connection to your news server every time you get new mail with Gnus. There is another way to start Gnus so that only the mail back ends are activated. Press M-x and type

$\underline{\text{gnus-no-server}}$

This command lets you read your mail offline. The next section demonstrates how you can effectively use Gnus as an offline news reader, an "unplugged" mode that is particularly useful for users connecting to the Internet intermittently with a slow modem.

# # Offline News Reading with the Gnus Agent

Recent versions of Gnus have included an entirely new mode of use called the Gnus Agent, also known as "Gnus Unplugged". The idea is for Gnus to download articles from selected subscribed newsgroups while you are online and then allow you to read them at your leisure and make follow-up replies while offline.

You can manually tag articles you want downloaded, or you can, with a little work, set up the Agent so that it downloads only messages that meet certain scoring criteria.

This sounds good, but be warned that configuring the Gnus Agent beyond the defaults requires some knowledge of Lisp if you want to go to selective about which articles are downloaded. Space doesn't permit me to go into advanced Agent configuration. The Gnus Info manual details the code needed to set up Agent categories, which could be a next step after absorbing and using the material in this section, although the simplified approach given here might be all you need.