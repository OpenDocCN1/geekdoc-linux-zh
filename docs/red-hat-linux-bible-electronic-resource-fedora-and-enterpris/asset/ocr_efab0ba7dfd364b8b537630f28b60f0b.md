A news server can be contentious as well. Without firm policies, you can find yourself dealing with demands for newsgroups from your users that may not be appropriate for your organization's goals.

# Which newsgroups should you offer?

After you decide to set up a news server, choosing the newsgroups to offer will have an impact on all other aspects of setting up the server. Your decision will affect the amount of traffic coming into the server, the disk space used, and probably, above all, how your users can spend or waste their time with newsgroups. Basically, you will do this by restricting which newsgroups are accepted from the news feeds you define. For example, you may want to exclude many of the newsgroups in the alt.* hierarchy because they include topics that are inappropriate in a business environment.

# How should articles be stored?

The traditional method of storing news articles places each article in a separate file within the news server's directory structure under the name of the newsgroup. This method is inefficient for large volumes of news. Therefore, INN offers several different methods of storing news articles. (See the section “Choosing How Articles Are Stored,” later in this chapter, for descriptions of each of these methods.)

# How long are articles stored?

Articles that are stored using the traditional news storage method are held for 10 days by default. You can change that value (by resetting entries in the `inn.conf` and `expire.ctl` files). For the `crlf` method, articles are rotated out automatically after the buffers are full. How to change the length of time that news articles are stored is described in detail later in this chapter.

# How do you find servers to provide your news feeds?

You need to find one or more news servers to provide you with news feeds. Likewise, you need to configure your news server to feed other news servers with the articles that you want to pass on. You can ask your ISP whether it can provide you with a news feed or query a newsgroup that discusses how to set up news servers. How to set up news feeds is described later in the chapter.

**TIP:** Some news feed providers don't want to be bothered with configuring partial news feeds. They will want you to take a full news feed or none at all. One way to use INN to configure a partial feed is by using the `suck` package. With `suck`, instead of having an INN server provide you with a feed, you simply use `suck` to copy selected newsgroups from an INN server. To do this, `suck` relies on the same command set that a standard INN newsgroup reader would use, but `suck` uses the results to populate its small INN server so multiple users can access the downloaded articles. You can find the `suck` package by visiting rmpind.net or a Red Hat FTP mirror site.