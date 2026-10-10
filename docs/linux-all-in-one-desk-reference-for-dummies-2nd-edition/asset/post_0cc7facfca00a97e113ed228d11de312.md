
2. **Type the names of the newsgroups, just as you would type the addresses of recipients when sending e-mail. Enter the subject and your message.**  
For this test posting, type *ignore* as the subject line and enter `misc.test` as the name of the newsgroup.  
Otherwise, any site that receives your article replies by mail to tell you the article has reached the site; that's in keeping with the purpose of the `misc.test` newsgroup.

3. **After you finish composing the message, click Send on the toolbar.**  
Thunderbird sends the message to the news server, which in turn sends it to other news servers, and soon it's all over the world!

4. **To verify that the test message reaches the newsgroup, choose File→Subscribe. Then subscribe to the `misc.test` newsgroup (that’s where you recently posted the new article). Look at the latest article (or one of the most recent ones) in `misc.test`; it should be the article you recently posted.**

If you post an article and read the newsgroup immediately, you see the new article, but that does not mean the article has reached other sites on the Internet. After all, your posting shows up on your news server immediately because that’s where you posted the article. Because of the store-and-forward model of news distribution, the news article gradually propagates from your news server to others around the world.

![](img/792720823146d68f19fd50c99ebfce4b_379_0.png)

The `misc.test` newsgroup provides a way to see whether news posting is really getting around. If you post to that newsgroup and don’t include the word *ignore* in the subject, news servers acknowledge receipt of the article by sending an e-mail message to the address listed in the Reply To field of the article’s header.

## Using KNode

Debian, MEPIS, and SUSE provide KNode as the default newsreader. Typically, you can start KNode by selecting Newsreader from the menu (look in the Internet applications). If you don’t see a choice for Newsreader in the menus, type `knode` in a terminal window to start KNode.

When KNode runs for the first time, it brings up the Configure KNode dialog box, shown in Figure 3-5, through which you can configure everything you need to read newsgroups and post items to newsgroups.

The left side of the dialog box shows all the items that you can configure, and the right side is where you enter the information for the item that you have currently selected on the left side.

## Reading Newsgroups from Your ISP

![](img/792720823146d68f19fd50c99ebfce4b_380_0.png)

Figure 3-5: Configure KNode from this dialog box.

When the Configure KNode dialog box first opens, it prompts for your personal information. Enter your identification information, such as name, e-mail address, and organization — this information is used when you post a new item to a newsgroup.

Then, click **Accounts** in the left side (refer to Figure 3-5) and click the Newsgroup Servers tab on the right side to set up information about the news server from which you will be reading news. Click **New** in the Newsgroup Servers tab to bring up a dialog box (see Figure 3-6) where you can enter the information about the news server. Your ISP should have provided you with the information needed to access the news server. If the news server requires a login name and a password, you must enter that information as well.

After you set up the news account, the KNode window shows the name of the news server in its left side, as shown in Figure 3-7. Right-click the server’s name and choose **Subscribe** to Newsgroups from the pop-up menu. A dialog box appears where you can subscribe to selected newsgroups (such as `comp.linux.announce`).

Figure 3-7 shows a typical view of the KNode window while reading an article from one of the subscribed newsgroups. The KNode user interface is similar to many other mail and newsreaders, including Thunderbird.

![](img/792720823146d68f19fd50c99ebfce4b_381_0.png)

![](img/792720823146d68f19fd50c99ebfce4b_381_1.png)

## Reading and Searching Newsgroups at Web Sites

If you don't have access to newsgroups through your ISP, you can still read newsgroups and post articles to newsgroups at a number of Web sites. Some of them archive old news articles and provide good search capabilities, so you can search these for articles related to some question you may have.

The best part about reading newsgroups through a Web site is that you don't even need access to a news server and you can read news from your Web browser.

Table 3-2 lists Web sites that offer free access to Usenet newsgroups. Some sites offer Usenet newsgroup service for a fee. I don't list them here, but you can search for them with Google (www.google.com) — type the search words **usenet newsgroup access** to get a list of all Web sites that offer newsgroup access (including the ones that charge a fee).

Table 3-2 Web Sites with Free Access to Usenet Newsgroups

| Web Site | URL |
| :--- | :--- |
| Google Groups | http://groups.google.com |
| mail2web | http://usenet.mail2web.com |
| InterBulletin | http://news.interbulletin.com |
| Usenet Replayer | www.usenet-replayer.com |
| Mailgate | www.mailgate.org |

One of the best places to read newsgroups, post articles, and search old newsgroup archives is Google Groups — Google's Usenet discussion forums — on the Web at `http://groups.google.com`. At that Web site, you can select a newsgroup to browse, and you can post replies to articles posted on various newsgroups.

The best part of Google Groups is the search capability. You already know how good Google's Web search is; you get that same comprehensive search capability to locate newsgroup postings that relate to your search words. To search newsgroups, fill in the search form at `http://groups.google.com` and press Enter.

To browse newsgroups in Google Groups, ignore the search box and look at the list of high-level newsgroup categories such as `alt`, `comp`, and `soc`. Click the category, and you can gradually drill down to specific newsgroups. When viewing an article in Google Groups, you can click a link that enables you to post a follow-up to that article.

![](img/792720823146d68f19fd50c99ebfce4b_382_0.png)

RSS stands for Really Simple Syndication. RSS is a format for *syndication* — gathering and making available — content of Web sites, primarily news-oriented sites and blogs. The term *blog* is short for *weblog* — a frequently updated journal with thoughts, comments, and opinions of the blog’s creator. RSS can be used to provide any kind of information that can be broken down into discrete items and put into RSS format. Such RSS-formatted content is called an *RSS feed*, and an RSS-aware program can check the feed periodically for changes, download new items, and make them available to the user.

The RSS format is a dialect of XML (eXtensible Markup Language). All RSS files conform to XML 1.0 specification.

There are many versions of RSS, but three versions — 0.91, 1.0, and 2.0 — are in widespread use. Netscape designed RSS version 0.90 for gathering and displaying headlines from news sites. A simpler version, 0.91, was proposed and UserLand Software picked up that version for use in its blogging product. At the same time, another noncommercial group had evolved RSS 0.90 into RSS 1.0, which is based on resource description format or RDF (see `www.w3.org/rdf`). UserLand did not accept RSS 1.0 but instead continued *evolving* RSS 0.91 through versions 0.92, 0.93, 0.94, and finally settled on RSS 2.0 (skipping 1.0 because that version number was already taken). Currently, many blogs and Web sites use RSS 0.91 for basic syndication (title, URL, and description); they use RSS 1.0 for readers that use RDF; and they use RSS 2.0 for advanced syndication with more metadata. (Think of metadata as *data about data*, which is what the RSS format provides: It provides data about other information, such as blogs and news.) RSS 1.0 files have a .rdf extension, whereas RSS 0.91 and 2.0 files have a .xml extension. However, all RSS files are text files that use XML tags.

![](img/792720823146d68f19fd50c99ebfce4b_383_0.png)

### Examining an RSS Feed

An RSS feed is a text file with XML tags that describe a Web site’s content. You typically use an automated program to periodically generate the RSS feed file, but you can prepare the RSS feed file using a text editor. It’s good to know what an RSS feed looks like, just so you can debug problems with the feed.

The specific details of an RSS feed depend on the version of RSS. The simplest feed is RSS 0.91 and here’s a typical RSS 0.91 feed:

```text
<?xml version="1.0" ?>
<!-- A comment line -->
<rss version="0.91">
```
