header is changed, while the content is intact. (Type **man Mail::SpamAssassin::Conf** to see other settings you can use in the `local.cf` file.)

Because there will almost certainly be some false-positives, you risk preventing your users from seeing an e-mail they need if you do system-wide filtering. To avoid this problem, the approach shown here lets the user decide what to do with e-mail tagged as spam.

Next, you should have the users of that mail server set up their own user preferences in their home directories. The preferences set in each user's `$HOME/.spamassassin/user_prefs` file help tell SpamAssassin how to behave for that user's e-mail. Here are examples of lines a user might want to have in that file:

```
required_hits               3
whitelist_from    jsmith@example.com  bjones@example.net
blacklist_from    *.example.org
```

The `required_hits` line (which is on by default) sets the number of hits needed to consider the message to be spam. Hits are based on scores for matching or not matching criteria in the tests SpamAssassin performs. (See `http://spamassassin.org/tests.html`.)

The `whitelist_from` and `blacklist_from` lines let you set addresses for people, individual hosts, or entire domains that should not be considered as spam (`whitelist_from`) or should always be considered as spam (`blacklist_from`). For other ways to modify SpamAssassin behavior, type the following command: **man Mail::SpamAssassin::Conf**.

At this point, SpamAssassin should be running and identifying spam based on input from you and the people using your e-mail server. Next, each user needs to decide what to do with the messages that are marked as spam, as described in the following section.

> **TIP:** Techniques you can use along with SpamAssassin include services like RealTime Blackhole Lists (RBL) and SpamCop. With RBL (`http://mail-abuse.org/rbl`), you can block spam messages before they even reach your server. SpamCop (`www.spamcop.net`) provides a service that allows you to enter spam messages you receive into a database that helps others block the same spam messages.

# Setting e-mail readers to filter spam

Each user can turn on filtering in his e-mail reader to decide what to do with each message tagged as spam from SpamAssassin. A common practice is to direct e-mail marked as spam to a separate folder. Because some real mail can occasionally be mistakenly marked as spam, you could check the spam folder every week or two, just to make sure you didn’t miss anything.

Here’s an example of how to add a filter rule from Evolution Email:

+   1. Create a folder labeled SPAM under your incoming mailbox.
+   2. Click Tools → Filters.