+   - OK accepts messages from the specified host, regardless of whether that host might fail other checks in the system (such as the anti-relaying provisions that we will discuss shortly).
+   - REJECT refuses connections initiated by the specified host.
+   - DISCARD silently drops messages after accepting them, making the sender think that the message has been successfully delivered.
+   - RELAY enables relaying for the specified host, overriding other checks (as with OK).
+   - 550 <message> specifies a "rejection" message that is displayed to a sender, matching the host specification. This message will appear during the SMTP session, and will be included in an error email message that is sent back to the sender.

After you've made changes to /etc/mail/access, the access.db file must be regenerated. This is done with the make maps target, which regenerates any of the feature map files that have been changed since the last time make maps has been run. Follow this command with make restart to restart the Sendmail master process with the new access.db file:

```
# make maps
/usr/sbin/makemap hash access.db < access
# make restart
/bin/kill -HUP `head -1 /var/run/sendmail.pid`
```

# Other Configuration Files

There are more files in /etc/mail that control Sendmail's operation: /etc/mail/virtusertable and /etc/mail/local-host-names are both important for advanced Sendmail configuration, such as an installation in which your server hosts email services for multiple domains. The virtusertable file allows you to set up mappings of user-names at other hosted domains to go to other local users' mailboxes at your normal domain; think of it as an aliases file on steroids. The local-host-names file allows you to specify which domains you're hosting mail for.

The complete documentation for how to use the virtual-hosting database and other configuration files can be found at http://www.sendmail.org, the Sendmail Consortium's Web site.

# Controlling Sendmail

Sendmail operates by keeping a single master process running and listening on port 25 for incoming connections—as well as additional processes for handling queue runs, sending messages to remote recipients, and other tasks. The master process is started at boot time from /etc/rc. Starting and stopping the Sendmail master process is made easy