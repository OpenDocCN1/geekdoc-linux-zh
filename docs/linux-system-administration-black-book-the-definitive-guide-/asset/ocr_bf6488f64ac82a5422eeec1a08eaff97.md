+   19. Choose the appropriate item under DNS Features:
+       - Click Wait For DNS if the machine has constant access to a domain name server.
+       - Click Don't Use DNS if the machine has intermittent or no direct access to a domain name server.

+   20. Click the Misc. tab to access its contents.

+   21. If you are using UUCP for some mail processing, do the following:
+       - Uncheck the No Batching For UUCP Mail option if you want email sent out at timed dial-up intervals rather than immediately.
+       - Change the number of bytes assigned to Max Size Of UUCP Messages if you want to make them larger or smaller. A single message exceeding this value will not be downloaded or uploaded. You can disable this by entering 0.

+   22. The Deliver Locally To Users text box contains a list of users that the mail server does not handle traffic for centrally. If you want anyone aside from the superuser handled this way—perhaps machine-specific administrative accounts are in use—add the usernames in this text box.

+   23. In addition to local delivery, you can choose to make it obvious to the recipient which host email came from for specific users. Once again, this is typically used for the superuser or particular administrative accounts. If you want this to work for more than root, add additional email addresses in the No Masquerade From Users text box.

+   24. Only add a username to the Trusted Users text box if you want this user to have access to your mail spools and queues.

+   25. If you want to apply special routing rules to your email delivery, check the Special Routing DB checkbox. This essentially activates the mailertable feature discussed previously in Table 12.6.

+   26. If you enable special routing, then you need to tell Linuxconf which database type you are using by selecting the proper entry in the Special Routing DB Format drop-down list box. The databases available are listed in Table 12.11.

+   27. Under Local Delivery Agent, choose procmail from the drop-down list box.

+   28. Unless you have a specific need to do so, do not check the Support Bogus Mail Clients option. This feature adds support for mail clients that send malformed greeting messages.

+   29. Click the Aliases tab to access its contents.

+   30. If you host any virtual domains, enter one domain.extension per text box. Clicking Add gives you additional text boxes.

+   31. Click the Accept button to save the changes. You are given the option of generating the new sendmail.cf file now or later.