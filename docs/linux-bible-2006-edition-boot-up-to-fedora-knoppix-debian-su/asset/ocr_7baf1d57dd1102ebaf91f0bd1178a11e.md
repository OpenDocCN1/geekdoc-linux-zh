# Part V ♦ Running Servers

```
warn message = X-Spam-Score: $spam_score ($spam_bar)
condition = ${$if <($message_size)(80k)[1](0)}
spam = nobody:true/defer_ok
warn message = X-Spam-Status: $spam_report
condition = ${$if <($message_size)(80k)[1](0)}
spam = nobody:true/defer_ok
```

The first block rejects messages that contain viruses or malware, and the second and third header handle messages indicating whether or not SpamAssassin considers them. The final block rejects messages having a spam score of higher than 12.
The defer_ok in the last three blocks tells Elm that it is to continue processing in the event that the SpamAssassin daemon could not be connected. You can remove it if you prefer to have the server return a temporary failure in such cases. You can also add /defer_ok to the end of the message = "line" if you want to continue processing in the event that a message cannot be scanned by ClamAV.

+   7. Tell Elm virus scanner to use and how to connect to SpamAssassin. Use a editor to create a file named /etc/exim4/conf.d/main/10_exim4-exiscan_acl_options that contains the following:
av_scanner = clamd:var/run/clamav/clamd.ctl
spam_address = 127.0.0.1:783

CHECK_DATA_LOCAL_ACL_FILE = CONFDIR/acl_check_data_local

+   8. Tell Elm to load the new configuration:
# invoke-rc.d exim4 reload

All messages transmitted through your server should now be checked for viruses using ClamAV. Additionally, messages with less than 80 kilobytes will also be checked using SpamAssassin. This is a good time to test the configuration again. Fixes for the problems you are most likely to encounter can be found in the next section.

# Testing and Troubleshooting

This section contains generic troubleshooting tips, specific information about some common errors and how to fix them.