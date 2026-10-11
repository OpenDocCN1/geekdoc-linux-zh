For example, the following hypothetical meeting is scheduled:
** Calendar Appointment **

+   - Date: 12/24/2001
+   - Start: 10:00 am
+   - End: 11:00 am
+   - What: Termination Meeting
+   - Manager and Employee Confidential

Now mail a message with this inside it. When the e-mail message arrives, the recipient can drag the entire e-mail message onto their Calendar application. The Calendar must be open at the time the message is dragged and dropped. Calendar will search through your e-mail for this text code so it can update your calendar at the same time. When it finds this text code in a message, it will update your Calendar to match the receiver's calendar.

This code section is not easy to read or create; the format has to be exact. There is one place where this comes in very handy. If you create a shell script that automatically mails out e-mail messages, include the calendar appointment text in the e-mail. You can then create a maintenance calendar on your desktop for your servers. If an e-mail comes in from one of your server's maintenance shell scripts and you decide to take action on the item, just drag and drop the mail message onto your calendar. This will automatically make a maintenance window visible on your calendar. Other system administrators and power users who browse your calendar can now see that you are going to work on the server performing some system maintenance. To add even more power, combine the calendar appointment text with some of Calendar's command-line options to automatically send out the e-mail message to everyone.

Calendar and Mailer have a lot more power and functionality than initially meets the eye.

# # Command-Line Utilities

The Calendar application is somewhat unique among calendar programs on other platforms in that it has several command-line utilities that can be run with shell scripts. These utilities can add, modify, display, and delete appointments on your schedule. If you use these shell scripts in conjunction with high-end text manipulation tools such as sed and awk, you can create very powerful calendar tools. You can also run these commands from a Telnet window or a command window.

One powerful use of these command-line utilities is that you can combine them with server maintenance. If you have a hard drive that has a constantly growing database, you can schedule maintenance times automatically on your calendar every time