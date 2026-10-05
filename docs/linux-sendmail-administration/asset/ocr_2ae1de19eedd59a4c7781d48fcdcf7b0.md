# 216 Chapter 7 The sendmail.cf File

This table, and this chapter, can help you read and understand the sendmail.cf file. But when it comes to creating that file, you'll build it with the m4 macro commands covered earlier in this book.

# Tell Me Again Why I Use m4 Macros

A persistent question raised by Sendmail administrators is, “Why not just edit sendmail.cf directly?” After all, is

```
define(`ALIAS_FILE`, `/etc/aliases`)
```

really any simpler than
0 AliasFile=/etc/aliases

The answer is no, individual m4 macros are not any simpler to read or write than individual sendmail.cf commands once you understand the meaning and syntax of the sendmail.cf commands. However, m4 macro configuration files are much shorter and easier to read than the sendmail.cf file, and individual m4 commands often do much more than individual sendmail.cf commands. m4 makes it possible to actual write a configuration from scratch. But you might not need to. Perhaps a sample sendmail.cf configuration provided by the Sendmail developers or your Linux vendor would work for you with only a few small changes. In case, why do I repeatedly insist that you build your configuration with m4?

The reason is “because that the way it’s done.” Everyone expects the Sendmail configuration to be defined in the m4 configuration file. That is where your colleagues will look for changes when they debug your system. Putting the configuration directly in the sendmail.cf file makes a confusing system more confusing to those who must debug it. Worse yet putting some changes in the macro configuration and some in sendmail.cf. That approach is doomed to failure. Stick with m4. It might not be simple, but it is better than the alternative and it is the way Sendmail configuration is done.