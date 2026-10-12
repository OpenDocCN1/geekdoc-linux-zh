```
# message_headers   [string_array] (undef) <resend,digest>
# These headers will be appended to the headers of the
# posted message. The text is expanded before being used.
# The following expansion tokens are defined: $LIST the
# name of the current list, $SENDER - the sender as taken
# from the from line, $VERSION, the version of majordomo.
message_headers  << END

END

# moderate          [bool] (no) <resend>
# If yes, all postings to the list  must be approved by the
# moderator.
moderate          =  no

# mungedomain       [bool] (no) <majordomo>
# If set to yes, a different method is used to determine a
# matching address. When set to yes, addresses of the form
# user@domain.ain.com are considered equivalent to addresses
# of the form user@ain.com. This allows a user to subscribe
# to a list using the domain address rather than the
# address assigned to a particular machine in the
# domain. This keyword affects the interpretation of
# addresses for subscribe, unsubscribe, and all private
# options.
mungedomain       =  no

# noadvertise       [regex_array] (undef) <majordomo>
# If the requestor name matches one of these regexps, then
# the list will not be listed in the output of a lists
# command. Noadvertise overrides advertise.
noadvertise       << END

END

# precedence        [word] (bulk) <resend,digest>
# Put a precedence header with value <value> into the
# outgoing message.
precedence        =  bulk

# private_get       [bool] (yes) <majordomo>
# If set to yes, then the requestor must be on the mailing
```