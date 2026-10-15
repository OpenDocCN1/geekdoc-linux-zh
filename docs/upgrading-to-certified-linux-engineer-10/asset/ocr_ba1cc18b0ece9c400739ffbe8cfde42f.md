8. Paste the content of the clipboard into the first terminal and do the following:

+   a. Press Enter.
+   b. Type . (dot).
+   c. Press Enter.

9. You should get a virus warning like the following one:

250 2.7.1 Ok, discarded, id=14069-01-2 - VIRUS: Eicar-Test-Signature

10. Enter quit.

# Part V - Send a Virus Email

+   1. Log in as user jgoldman by entering su - jgoldman.
+   2. Send a virus mail to user tux by entering mail geeko@digitalairlines.com < /usr/share/doc/packages/amavisd-new/test-messages/sample-virus-simple.txt
+   3. Log out by entering exit.
+   4. As root, enter mail to look for new email.

There should be an email from virusalert in your mail folder.

(End of Exercise)