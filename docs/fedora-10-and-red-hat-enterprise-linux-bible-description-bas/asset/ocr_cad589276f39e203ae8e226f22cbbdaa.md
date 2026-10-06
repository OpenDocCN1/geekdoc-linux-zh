# Chapter 19: Setting Up a Mail Server 817

| required_score | 3 |
| whitelist_from | jsmith@example.com bjones@example.net |
| blacklist_from | *.example.org |

The required_score line (which is set to 5 by default, but set to 3 here) sets the score needed to consider the message to be spam. Scores are based on matching or not matching criteria in the SpamAssassin filters. See http://spamassassin.apache.org/tests.html.

The whitelist_from and blacklist_from lines let you set addresses for people, hosts, or entire domains that should not be considered as spam (whitelist_from) or should always be considered as spam (blacklist_from). For other ways to modify SpamAssassin behavior, type the following:

```
man SpamAssassin::Conf
```

At this point, SpamAssassin should be running and identifying spam based on input from you and the people using your e-mail server. Next, each user needs to decide what to do with the messages that are marked as spam, as described in the following section.

> TIP: Techniques you can use along with Spam include services such as SpamCop. SpamCop (http://www.spamcop.net) provides a service that allows you to enter spam messages into a database that helps block other spam messages.

# Setting e-mail readers to filter spam

Each user can turn on filtering in his or e-mail reader to decide what to do with each message tagged as spam by SpamAssassin. A common practice is to direct e-mail marked spam to a separate folder. Because real mail can be mistakenly marked as spam, you can check the spam folder every week or two, just to make sure you don't miss anything.

Here's an example of how to add a filter rule in Evolution:

+   1. Create a folder labeled Spam under your incoming mailbox.
2. Click Edit ⇨ Filters.
3. From the Filters window, click Add Rule window appears.
4. Identify a rule name (such as spam) that a criterion that looks for a specific header (X-Spam-Flag) containing specific text (YES). Then under Add Action, select an action (Move to Folder) and identify the folder to contain the spam messages (SPAM).

When you ask to receive mail from your mail server, all messages with the X-Spam-Flag set to yes are sorted into your SPAM folder. As an alternative, you can check for the [SPAM] to appear in the subject line as the criterion for sorting the spam messages.

Other mail readers (Sea Monkey, pine, Netscape, and others) also include features for filtering and sorting e-mail based on criteria you enter.