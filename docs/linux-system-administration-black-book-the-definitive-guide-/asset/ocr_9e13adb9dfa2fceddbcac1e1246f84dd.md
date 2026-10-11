# **Table 12.13** **Results available in*access.db*.


| Result | Purpose |
| :--- | :--- |
| ### text | Rejects with an error response. The hash marks refer to a three-digit error code, and **text** is a response you include. The error code comes from RFC 821, which you can find at [www.faqs.org/rfcs/rfc821.html](http://www.faqs.org/rfcs/rfc821.html). Search for the text "4.2.1. REPLY CODES BY FUNCTION GROUPS" to find the error code listing. |
| DISCARD | Tosses out any mail that matches this rule. |
| OK | Accepts this mail. Overrides any other rules that might reject it. |
| REJECT | Bounces the mail with a general error message. |
| RELAY | Allows relaying for mail matching these rules. |


+   5.  When you are finished, press the Esc key, and then type "ZZ" to save and close the file.
+   6.  Type "/etc/rc.d/init.d/sendmail restart" to restart the mail daemon.

# ## Removing Mail From The Queue Under Linuxconf

To alter your mail queue using Linuxconf, do the following:

+   1.  Enter GNOME as root.
+   2.  Click the footprint icon to open the main menu.
+   3.  Click System|Linuxconf to open the Linuxconf configuration tool.
+   4.  Expand Config|Server Tasks|Mail Delivery System (Sendmail) and then expand the Basic section.
+   5.  Click The Mail Queue to open the Mail Queue dialog box, shown in Figure 12.13.
+   6.  Click an entry in the dialog box to view its contents. You do not actually see the body of the email here. Instead, you see its size, its queue status, the sender, and the date it was sent. This is a good way to see if something got stuck in the queue.
+   7.  To remove this entry from the queue, click the Del button in the entry's dialog box. Otherwise, click Cancel.
+   8.  Click Quit to close the Mail Queue dialog box.