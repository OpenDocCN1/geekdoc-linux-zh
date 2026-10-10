
![](img/11709a8f88c8cd03868a929dc94c0e2b_375_0.png)

My discussion of reading newsgroups assumes that you obtained access to a news server from your ISP. The ISP provides you the name of the news server and any username and password needed to set up your news account on the newsreader you use.

To read news, you need *a newsreader* — a program that enables you to select a newsgroup and view the items in that newsgroup. You also have to understand the newsgroup hierarchy and naming conventions (which I describe in the “Newsgroup hierarchy” section, earlier in this chapter). Now I show you how to read news from a news server.

![](img/11709a8f88c8cd03868a929dc94c0e2b_375_1.png)

If you don’t have access to newsgroups through your ISP, you can try using one of the many public news servers that are out there. For a list of public news servers, visit NewzBot at `www.newzbot.com`. At this Web site, you can search for news servers that carry specific newsgroups.

### Taking stock of newsreaders

You can use one of several software packages that enable you to download and read newsgroups in Linux. Here are a few major newsreaders:

- **Thunderbird**: Thunderbird includes the ability to download news from an NNTP server. You can read newsgroups and post items to newsgroups. Xandros uses Thunderbird for mail and news.
- **KNode**: This is a newsreader for KDE that you can download from `knode.sourceforge.net`. Debian, MEPIS, and SUSE provide KNode as the newsreader.
- **Pan**: Pan is a GUI newsreader that, according to the developer’s Web site (`http://pan.rebelbase.com`), “… attempts to be pleasing to both new and experienced users.” You can download Pan for various Linux distributions from `http://pan.rebelbase.com/download`.

![](img/11709a8f88c8cd03868a929dc94c0e2b_375_2.png)

If you don’t find a newsreader in your Linux system, you can download and install any of these newsreaders easily in any of the Linux distributions. Often, you can locate the download site by a simple search at a search engine — just search for the word *download* followed by the name of the newsreader.

### Reading newsgroups with Thunderbird

You can browse newsgroups and post articles from Thunderbird, a mail and newsreader from the Mozilla project.

![](img/11709a8f88c8cd03868a929dc94c0e2b_375_3.png)

In some distributions such as Xandros, the Main Menu has options to start Thunderbird directly. In many Linux distributions, the mail and news component of Thunderbird may not be installed. In that case, you have to download and install the Thunderbird mail and news component or use another newsreader.

When you’re starting to read newsgroups with Thunderbird for the first time, follow these steps to set up the news account:

1. **Choose Edit > Account Settings from the Thunderbird menu.** A dialog box appears.
2. **Click Add Account.** The Account Wizard appears, as shown in Figure 3-2.

![](img/11709a8f88c8cd03868a929dc94c0e2b_376_0.png)

Figure 3-2: Thunderbird’s Account Wizard guides you through the newsgroup account setup.

3. **Select the Newsgroup Account radio button** (refer to Figure 3-2) **and click Next.**
4. **In the new screen that appears, fill in your identity information — name and e-mail address — and click Next** to move to the next screen.
5. **Enter your news server name and click Next.**
6. **Enter a descriptive name of the newsgroup account and click Next.**
7. **Click Finish to complete the newsgroup account setup.**

The new newsgroup account now appears in the list of accounts on the left side of the Thunderbird window. Click the newsgroup account name, and the right side of the window shows the options for the newsgroup account.

Click the Subscribe to Newsgroups link. Thunderbird starts to download the list of newsgroups from the news server.

![](img/11709a8f88c8cd03868a929dc94c0e2b_377_0.png)

If your ISP’s news server requires a username and password, you’re prompted for that information. After that, Thunderbird downloads the list of newsgroups and displays them in the Subscribe dialog box. (You can enter a search string in a text box to narrow the list.) When you find the newsgroups you want, click the check box to subscribe to these newsgroups, as shown in Figure 3-3. Then click OK to close the dialog box.

![](img/11709a8f88c8cd03868a929dc94c0e2b_377_1.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_377_2.png)

After you subscribe to newsgroups, these newsgroups appear under the newsgroup account name in the left side of the Thunderbird window. You can then read a newsgroup using these steps:

1. **Click a newsgroup name** (for example, comp.os.linux.announce). If your news server requires a username and password, a dialog box prompts you for this information. Then another dialog box asks you how many message headers you want to download.
2. **Specify the number of headers** (for example, 500) you want and click Download to proceed. Thunderbird downloads the headers from the newsgroup and displays a list in the upper-right area of the window.
3. **From the list of headers, click an item to read that article, as shown in Figure 3-4.**

To select other subscribed newsgroups, simply click the newsgroup’s name in the left side of the window.

![](img/11709a8f88c8cd03868a929dc94c0e2b_378_0.png)

Figure 3-4: Click an article to read it in the lower-right part of the window.

# Newsgroup subscriptions

Unlike magazines or newspapers, newsgroups don’t require that you subscribe to them; you can read any available newsgroup on the news server. The news server’s administrator may decide to exclude certain newsgroups, however; if they aren’t included, you cannot read them.

The only thing that can be called *subscribing* is indicating the newsgroups you routinely want to read. The news server does not receive any of this subscription information — the information is used only by the newsreader to determine what to download from the news server.

# Posting news

You can use any newsreader to post a news article (a new item or a reply to an old posting) to one or more newsgroups. The exact command for posting a news item depends on the newsreader. For example, in the Thunderbird newsreader, you follow these steps to post an article:

1. Click the **Reply** button on the toolbar to post a follow-up to a news item you’re reading. To post a new news article, click the **Compose** button. A window appears where you can compose the message.

Book IV
Chapter 3
Reading
Newsgroups and
RSS Feeds

## **354 Reading Newsgroups from Your ISP**

2. **Type the names of the newsgroups, just as you would type the addresses of recipients when sending e-mail. Enter the subject and your message.**

   For this test posting, type `ignore` as the subject line and enter `misc.test` as the name of the newsgroup. Otherwise, any site that receives your article replies by mail to tell you the article has reached the site; that’s in keeping with the purpose of the `misc.test` newsgroup.

3. **After you finish composing the message, click Send on the toolbar.**

   Thunderbird sends the message to the news server, which in turn sends it to other news servers, and soon it’s all over the world!

4. **To verify that the test message reaches the newsgroup, choose File Subscribe. Then subscribe to the `misc.test` newsgroup (that’s where you recently posted the new article). Look at the latest article (or one of the most recent ones) in `misc.test`; it should be the article you recently posted.**

If you post an article and read the newsgroup immediately, you see the new article, but that does not mean the article has reached other sites on the Internet. After all, your posting shows up on your news server immediately because that’s where you posted the article. Because of the store-and-forward model of news distribution, the news article gradually propagates from your news server to others around the world.

![](img/11709a8f88c8cd03868a929dc94c0e2b_379_0.png)

The `misc.test` newsgroup provides a way to see whether your news posting is really getting around. If you post to that newsgroup and don’t include the word `ignore` in the subject, news servers acknowledge receipt of the article by sending an e-mail message to the address listed in the Reply To field of the article’s header.

# **Using KNode**

Debian, MEPIS, and SUSE provide KNode as the default newsreader. Typically, you can start KNode by selecting Newsreader from the menu (look in the Internet applications). If you don’t see a choice for Newsreader in the menus, type `knode` in a terminal window to start KNode.

When KNode runs for the first time, it brings up the Configure KNode dialog box, shown in Figure 3-5, through which you can configure everything you need to read newsgroups and post items to newsgroups.

The left side of the dialog box shows all the items that you can configure, and the right side is where you enter the information for the item that you have currently selected on the left side.
