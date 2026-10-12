
Click the Subscribe to newsgroups link. Mozilla Mail starts to download the list of newsgroups from the news server.

If your ISP's news server requires a user name and password, you're prompted for that information. After that, Mozilla Mail downloads the list of newsgroups and displays them in the Subscribe dialog box. (You can enter a search string in a text box to narrow the list.) When you find the newsgroups you want, mark the check box to subscribe to these newsgroups (as in Figure 3-3). Then click OK to close the dialog box.

Figure 3-3:
Indicate which newsgroups you want to subscribe to in this dialog box.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_412_0.png)

After you subscribe to newsgroups, these newsgroups appear under the newsgroup account name in the left side of the Mozilla Mail window. You can then read a newsgroup using these steps:

- 1. **Click a newsgroup name (for example, `comp.os.linux.announce`).**
- This brings up a dialog box that asks you how many message headers you want to download.
- 2. **Specify the number of headers (for example, 500) you want and then click OK to proceed.**
- Mozilla Mail downloads the headers from the newsgroup and displays a list in the upper-right area of the window.
- 3. **From the list of headers, click an item to read that article (as in Figure 3-4).**

To select other subscribed newsgroups, simply click the newsgroup's name in the left side of the window.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_413_0.png)

Figure 3-4:
Click an article to read it in the lower right hand window.

## Newsgroup subscriptions

Unlike magazines or newspapers, newsgroups don't require that you subscribe to them; you can read any newsgroup that is available on the news server. The news server's administrator may decide to exclude certain newsgroups. If they aren't included, however, you cannot read them.

The only thing that can be called "subscribing" is when you indicate the newsgroups you routinely want to read. The news server does not receive any of this subscription information — the information is used only by the newsreader to determine what to download from the news server.

## How to post news

You can use any newsreader to post a news article (a new item or a reply to an old posting) to one or more newsgroups. The exact command for posting a news item depends on the newsreader. For example, in the Mozilla Mail newsreader, you follow these steps to post an article:

- 1. **Click Reply on the toolbar to post a follow-up to a news item you're reading.** To post a new news article, click Compose.
- A window appears where you can compose the message.
- 2. **Type the names of the newsgroups, just as you type the addresses of recipients when sending e-mail; then enter the subject and your message.**

For this test posting, type `ignore` as the subject line and enter `misc.test` as the name of the newsgroup.

Otherwise, any site that receives your article replies by mail to tell you the article has reached the site; that's in keeping with the purpose of the `misc.test` newsgroup. Figure 3-5 shows the message being composed in Netscape Communicator.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_414_0.png)

Figure 3-5:
You can post follow-ups or new news articles from Mozilla Mail newsreader.

3. After you finish composing the message, click Send on the toolbar (see Figure 3-5).

Mozilla Mail sends the message to the news server, which in turn sends it to other news servers, and soon it's all over the world!

4. To verify that the test message has reached the newsgroup, choose File→Subscribe; then subscribe to the `misc.test` newsgroup (that's where you've recently posted the new article). Look at the latest article (or one of the most recent ones) in `misc.test`, which should be the article you've recently posted.

If you post an article and read the newsgroup immediately, you see the new article, but that does not mean the article has reached other sites on the Internet. After all, your posting shows up on your news server immediately because that's where you posted the article. Because of the store-and-forward model of news distribution, the news article gradually propagates from your news server to others around the world.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_414_1.png)

The `misc.test` newsgroup provides a way to see whether or not your news posting is really getting around. If you post to that newsgroup and don't include the word ignore in the subject, news servers acknowledge receipt of the article by sending an e-mail message to the address listed in the Reply To field of the article's header.

## Reading and Searching Newsgroups at Web Sites

If you don't have access to newsgroups through your ISP, you can still read newsgroups and post articles to newsgroups at a number of Web sites. Some of them archive old news articles and provide good search capabilities, so you can search these for articles related to some question you may have.

The best part about reading newsgroups through a Web site is that you don't even need access to a news server and you can read news from your Web browser.

Table 3-2 lists Web sites that offer free access to Usenet newsgroups. There are some sites that offer Usenet newsgroup service for a fee. I don't list them here, but you can search for them in Google (www.google.com) — type the search words usenet newsgroup access and you should get a list of all Web sites that offer newsgroup access (including the ones that charge a fee).

**Table 3-2 Web Sites with Free Access to Usenet Newsgroups**

| Web Site | URL |
|---|---|
| Google Groups | groups.google.com |
| NewsOne.Net | newsone.net |
| Mailgate | www.mailgate.org |

One of the best places to read newsgroups, post articles, and search old newsgroup archives is Google Groups — the Google Usenet discussion forums — on the Web at groups.google.com. At that Web site, you can select a newsgroup to browse and you can post replies to articles posted on various newsgroups.

The best part of Google Groups is the search capability. You already know how good Google's Web search is; you get that same comprehensive search capability to locate newsgroup postings that relate to your search words. To search newsgroups, fill in the search form at groups.google.com and press Enter.

To browse newsgroups in Google Groups, ignore the search box and look at the list of high-level newsgroup categories such as alt, comp, and soc. Click the category, and you can gradually drill down to specific newsgroups. When viewing an article in Google Groups, you can click a link that enables you to post a follow-up to that article.

## Chapter 4: Transferring Files with FTP

### In This Chapter

- Using the GNOME FTP client
- Using the Mozilla Web browser as FTP client
- Learning to use the FTP command

Just as the name implies, *File Transfer Protocol* (FTP) is used to transfer files between computers. For example, if your Internet service provider (ISP) gives you space for a personal Web page, you may have already used FTP to upload the Web page. Using an FTP client on your computer, you log in to your ISP account, provide your password, and then copy the files from your home system to the ISP's server.

You can also use FTP to download other files anonymously, such as open-source software from other computers on the Internet — in which case, you don't need an account on the remote system to download files. You can simply log in using the word `anonymous` as the user name and provide your e-mail address as the password (in fact, your Web browser can do this on your behalf, so you may not even know this is happening). This type of anonymous FTP is great for distributing files to anyone who wants them. For example, a hardware vendor might use anonymous FTP to provide updated device drivers to anyone who needs them.

Red Hat Linux comes with several FTP clients, both command-line ones and GUI ones. In this chapter, I introduce you to a few GUI FTP clients and, for the command-line FTP client, I describe the commands you use to work with remote directories.

## Using Graphical FTP Clients

You can use one of the following GUI FTP clients in Red Hat Linux:

- gFTP — a graphical FTP client
- Mozilla Web browser for anonymous FTP downloads
