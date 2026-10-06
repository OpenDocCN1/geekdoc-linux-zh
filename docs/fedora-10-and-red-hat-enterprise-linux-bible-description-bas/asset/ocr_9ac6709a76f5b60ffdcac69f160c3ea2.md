# Chapter 19: Setting Up a Mail Server 823

You can leave these values as fqdn to simply use the local computer's fully qualified domain name.

+   Edit the /etc/conf.d/mailman.conf file. To cause queries, uncomment the RedirectMatch line at the bottom of the file and change that to include your fully qualified domain name. For example, when I did this for linuxtoys.net mailing list, the line appeared as follows:
```RedirectMatch ^/mailman/(.*)$ http://linuxuxtoys.net/mailman/listinfo\```
To create a mailing list, you must first create an unpopulated mailing list mailman. With that, you must enter the e-mail and initial password for the person responsible for administering the list. To do that, type the following:
```# /usr/lib/mailman/bin/newlist mailman
Enter the email of the person running the list: chris@linuxuxtoys.net
Initial mailman password: ********nEnter to notify mailman owner...\```

+   Restart the Web (httpd) service and start the mailing list as follows:
```# service httpd restart
# service mailman start
# httpconfig config on\```
Create a new mailing list, using the newlist command as follows:
```# /usr/lib/mailman/bin/newlist
Enter the email of the list: pro
Enter the email of the person running the list: chris@linuxuxtoys.net
Initial password: ******
To finish creating your mailing list, you must edit /etc/aliases (or equivalent) file by adding the following lines, and running the 'newaliases' program\```

```
## pro mailing list
pro: |/usr/lib/mailman/mail/mailman post pro"
pro-admin: |/usr/lib/mailman/mail/mailman admin pro"
pro-bounces: |/usr/lib/mailman/mail/mailman bounces pro"
pro-confirm: |/usr/lib/mailman/mail/mailman confirm pro"
pro-join: |/usr/lib/mailman/mail/mailman join pro"
pro-leave: |/usr/lib/mailman/mail/mailman leave pro"
pro-owner: |/usr/lib/mailman/mail/mailman owner pro"
pro-request: |/usr/lib/mailman/mail/mailman request pro"
pro-subscribe: |/usr/lib/mailman/mail/mailman subscribe pro"
pro-unsubscribe: |/usr/lib/mailman/mail/mailman unsubscribe pro"
```

+   Copy and paste the text just shown (starting from the line ## projectlist mailing list) into the end of your /etc/aliases file.