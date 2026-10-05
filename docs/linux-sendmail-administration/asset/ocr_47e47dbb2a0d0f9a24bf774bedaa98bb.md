+   Use either the genericstable or the user database to process sender addresses, do not use both. If you use the user database, do not maildrop commands to replicate recipient names already covered by the aliases database.

+   Use the access database to control mail delivery and replying. It provides finer control than the relay-domains. Only use relay-domains where it is adequate to the task, such as on small departmental systems that don't need the full range of services provided by the access database.

+   Use virtertable only if you truly need to support virtual domains. This database probably only applies to e-business sites and ISPs.

+   Use the mailertable only if you use procmail for non-local mail. Most other users of the mailertable are less than optimal solutions for real problems. For example, upgrading the external system to accept Extended SMTP is a better solution than using the mailertable to force mail through smtp8.

+   Solve DNS transition problems with proper DNS configuration. Avoid using domaintable as anything other than a short-term fix.

+   Don't use the trusted-users file, the bitdomain database, or the uucpdomain database.

The Sendmail databases are the final topic in Part 2, "Essential Configuration," and they are the most frequently used tools of basic configuration. The next chapter, "sendmail1.cf File," begins Part 3, "Advanced Configuration." Considering the complexity that we have already seen, and the advanced nature of the skills needed to master this complexity, it might be hard to believe things could get more advanced. But they can. In the next part of this book, we drill deeper into the configuration and look at ways we can customize Sendmail at this deep level.