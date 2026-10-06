# FIGURE 26-7

Using KMail to view a message with an attachment

![](bbox=[0.131, 0.172, 0.868, 0.542])

This command sends the system log file as an attachment to the e-mail address rich on the local system. Note that you must also have the proper permissions to access the e-mail message you want to attach. Figure 26-7 shows the received-email message in the KMail client.

Notice that the message includes the body text from the echo statement, along with a separate icon for the attached file. You can save the attached file directly from the KMail client.

> > If you click at the name of the attached file, you will notice that Mutt uses the basename of the attached file as the filename in the attachment. Be careful Mutt will use the temporary filename as the attachment filename. You'll be better off saving temporary files using more descriptive names rather than using temporary filenames.

# Summary

This chapter discusses how to incorporate e-mail in your shell scripts. The ability to regularly e-mail reports to customers is a great feature to offer in your shell scripts.