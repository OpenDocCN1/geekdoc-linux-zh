8. If the NetMail Service is configured to use a different eDirectory tree than your Virtual Office server, then mark **Different than the Virtual Office Tree**. This will require users to provide a user name and password to authenticate to NetMail when they select the eMail link in the Virtual Office home page.

9. Click OK.

10. If you want the Reduced eMail field displayed on users' Virtual Office home page, complete the following:

> NOTE
> The Reduced eMail View gadget doesn't use NetMail's Modular Web Agent the way the eMail link (configured previously) does. Instead, it uses either the POP3 or IMAP protocol to access your NetMail server. To use this, then you need to make sure you have configured a POP or IMAP Agent for your NetMail server.

+   a. Mark **Enable** on the **Home Page Reduced eMail View** line.
+   b. Click **Edit**. The screen in Figure 11.28 is displayed.

![](bbox=[0.16, 0.47, 0.95, 0.78])

+   c. Under **Mail Server Type**, select the protocol that will be used to access your NetMail server. Your choice will depend on the NetMail agents you've deployed.
+   d. In the **Incoming Mail Server DNS Name** field, the default address of %*serverdnsnoport% is displayed. As mentioned earlier, the text %*serverdnsnoport% is a variable that is replaced with the address of the same server where Virtual Office is