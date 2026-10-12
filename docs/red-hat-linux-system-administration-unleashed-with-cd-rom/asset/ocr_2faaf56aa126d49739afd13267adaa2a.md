```
# or daemon

# user - match users on the local host with delivery to their
# mailboxes
user:  driver = user;        # driver to match usernames

transport = local          # local transport goes to mailboxes

# real_user - match usernames when prefixed with the string "real-"
#
# This is useful for allowing an address which explicitly
# delivers to a user's mailbox file. For example, errors in a
# .forward file expansion can be delivered here, or forwarding
# loops between multiple machines can be resolved by using a
# real-username address.
real_user:
  driver = user;
  transport = local,
  prefix = "real-."        # for example, match real-root

# let users put mailing lists on their local machines
private_lists:
  caution,
  owner=owner-$user,
  driver=forwardfile;
  file=/private/usr/lib/smail/lists/${lc:user}

# lists - expand mailing lists stored in a list directory
#
# mailing lists can be created simply by creating a file in the
# /usr/lib/smail/lists directory.
lists:  driver = forwardfile,
  caution,
  # flag all addresses with
  # caution
  nobody,                 # and then associate the
  # nobody user
  owner = owner$User;

# map the name of the mailing list to lower case
file = lists/${lc:user}

# smart_user - a partially specified smartuser director
#
```