In this sample file, the user1@client-1.com address has been mapped to the local account client1, the webmaster@client-1.com has been mapped to a remote ISP account, and all other possible e-mail addresses for the domain have been mapped to the local account. The last entry is quite useful and often requested. It allows the client-1.com domain to use whatever e-mail address they want on their Web site or other business publications and advertising and still get the mail in the right place. For example, if www.client-1.com publishes an e-mail address called info@client-1.com, anyone sending mail to that account is happily serviced by the client1 user.

+   ■ Now create the /etc/mail/client-b.ftr file for the second client. This file is likely to be similar to the previous example, but suppose that the client-b.com owner wants all e-mail addresses to be automatically mapped to her existing accounts in your hometown ISP mail server. In such a case this map file will look as follows:
+   
+   `@client-b.com $1@home-town-isp.com`
+   
+   ■ Now that you have two virtual user map files, you can create the final /etc/mail/virtusertable file using the following commands:
+   
+   `touch /etc/mail/virtusertable`
+   
+   `cat *.ftr > /etc/mail/virtusertable`
+   
+   Here, the first command creates the /etc/mail/virtusertable file if it does not already exist. The second command concatenates all the .ftr files to /etc/mail/virtusertable. This effectively creates the final /etc/mail/virtusertable.
+   
+   ■ Now you can run the makemap program to create the database version of the file as follows:
+   
+   `makemap hash /etc/mail/virtusertable < /etc/mail/virtusertable`

As you can see in the preceding example, creating multiple virtual user map files can help you to keep track of individual domains quite easily. Any time you want to change a domain specific map, just modify the domain's ftr file and create the final /etc/mail/virtusertable file using the technique discussed here.