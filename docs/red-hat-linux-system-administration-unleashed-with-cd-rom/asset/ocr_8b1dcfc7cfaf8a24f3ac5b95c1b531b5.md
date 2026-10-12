```
# list in order to get files.
private_get      = yes

# private_index    [bool] (no) <majordomo>
# If set to yes, then the requestor must be on the mailing
# list in order to get a file index.
private_index    = yes

# private_info      [bool] (no) <majordomo>
# If set to yes, then the requestor must be on the mailing
# list to use the info <list> command.
private_info     = no
# private_which     [bool] (no) <majordomo>
# If set to yes, then the requestor must be on the mailing
# list in order to get which info from that list.
private_which    = no

# private_who       [bool] (no) <majordomo>
# If set to yes, then the requestor must be on mailing the
# list in order to use the who command.
private_who      = yes

# purge_received    [bool] (no) <resend>
# Remove all received lines before resending the message.
purge_received   = no

# reply_to          [word] () <resend,digest>
# Put a reply-to header with value <value> into the
# outgoing message. If the token $SENDER is used, then the
# address of the sender is used as the value of the reply
# to header. This is the value of the replyto header for
# digest lists.
reply_to         =

# resend_host       [word] (undef) <resend>
# The host name that is appended to all address strings
# specified for resend.
resend_host      =
```