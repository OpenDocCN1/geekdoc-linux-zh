# Responding to Email with procmail

procmail can help you automatically—or selectively—respond to email. As you’ll see, procmail is very similar to forwarding email and using the vacation program, but you’ll probably find procmail much more flexible.

# To specify how messages should be filtered (to "write a recipe"):

+   1. vi ~/.procmailrc
+      In vi, access your .procmailrc file.
+   2. Move to the end of the file, below the setup information.
+   3. :0:
+      Start a new recipe with :0:, as shown in Figure 11.18. (Don’t ask why to use :0:. That’s just the way it is.)
+   4. * ^TOGolfBuddies
+      Set the criteria for procmail to filter with. Here.
+      ▲ * ^TO tells procmail to examine the TO line (and, actually, the CC line, too) of all incoming messages.
+      ▲ GolfBuddies is the text to match in the TO line (as in TO: GolfBuddies@nowhere.nowhen.com). Of course, you’d put in the actual name of the list to look for (or the alias for your mailing list, or whatever), rather than GolfBuddies.
+   5. $MAILDIR/FriGolfBuddies
+      Specify where the filtered mail should go. In this case, filtered mail would go in the FriGolfBuddies folder, but you might filter messages from mailing lists into a listmail folder.
+   6. Save and close the file.

![](bbox=[0.58, 0.07, 0.93, 0.38])