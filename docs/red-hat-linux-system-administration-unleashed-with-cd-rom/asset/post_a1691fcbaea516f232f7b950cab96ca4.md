
To find out more information, check out the home page at http://www.acme.com/software/thttpd/.

## WN

WN is a very full-featured Web server that is distributed for free under the GPL. It supports HTTP/1.1 and also has some very advanced features that are normally only available under CGI programs. WN was designed with the following three goals in mind: security, robustness, and flexibility.

WN has the following advanced features built in:

- **Searching**— WN has excellent navigational aids built into the server, including title searches, list searches, index searches, keyword searches, and context searches.
- **Parsed Text, Server-Side Includes and Wrappers**— WN has the ability to insert text into files being served. It also has full support for server-side includes and wrappers.
- **Filters**— You can apply filters to any files being served by WN. A filter can parse and modify a file before it's served, and can accomplish stuff like on-the-fly compression and decompression.
- **Ranges**— When accessing a file from a WN server, a range can be supplied and only the line numbers within that range will be displayed.

The WN home page is located at http://hopf.math.nwu.edu/.

## Summary

In this chapter, we examined Web serving under Red Hat Linux. In particular, we looked at the Apache Web server, Squid, and some alternatives to Apache. You should have a good idea of how to go about configuring both Apache and Squid.

This chapter only lays the groundwork for getting started using Linux as a Web server. I trust your journey into the world of Web serving will not end here. There are many books and lots of online documentation available that will allow you to explore this topic extensively.

## News Services

### In This Chapter

- So You Want to Run a News Server? 672
- INN and Friends 676
- News Clients 705
- Places to Ask Questions and Find Answers 711

This chapter discusses a bit of the history of Usenet, how it works, and what it takes to run a Usenet server. We’ll only discuss a few of the software packages you can use for this, but there are several ways to use any Usenet server software.

## So You Want to Run a News Server?

Usenet news started when two departments on opposite sides of a college campus decided they wanted to exchange bulletin board postings. They wrote some software that exchanged posts to each others’ servers, and that evolved over time into what we now know as Usenet news.

How does it work? Each message has two pieces of information that keep the message from being duplicated: the Path header and the message-id. The Path header tells you where this article has been so that you don’t send it back to where it came from. That would be a waste of time and bandwidth. The message-id is a pseudo-unique message identifier. The message-id is usually based on a timestamp and the host from which the message was posted. A typical message-id would look like <12345@hostname.domain.com>. Each news server keeps track of the message-ids it has or has seen recently. If the server is offered a message with a duplicate message-id, the server refuses that article. A decent sized private server usually will keep between one and two million articles on hand at any given time. The size of a typical article may vary widely. In any event, you can see that a news server is going to use a lot of resources.

## Capacity Planning

There are two things to consider when thinking about the capacity of a Usenet server. The disk capacity of the system that will be the server is the most obvious, but you must also consider the capacity of the Internet connection to the site at which the server will reside.

### Server Storage Capacity

A full newsfeed (I hope you are sitting down) can exceed 30GB a day. Yes, that’s gigabytes! That’s more bandwidth than a full T1. Mind you, that includes all the binary newsgroups and all the commercial spam that nobody really wants to read. After filtering all that out, it gets down to a much more manageable number—usually less than a gigabyte a day. If you want to carry the binaries, you will need much more disk storage. We’ll talk more about this in the discussion on tweaking a server, but you should consider using two or more disks for a Usenet server regardless of the size.

Now we get down to the meat of it. How much disk space do you really need? Well, that depends. That depends on how long you want to have the news around. Let’s say you get a feed based on what your users will be interested in. Start with comp.*, rec.*, and soc.*. That should be about 100-200MB/day. Let’s use 150MB as a round number for calculations. If you want to keep articles for two weeks (a reasonable time), your news spool will be 2100MB, or about 2.0GB. However, that’s just for your news spool (where the articles are stored). You will also have to allocate space for your history database (so the server remembers which articles it has). A good way to figure that is to allow about 100 bytes for each article. Articles from this newsfeed (comp.*, rec.*, soc.*) should be about the average article size, around 3KB. You do the math and figure that a 2GB news spool will hold about 700,000 articles. So, at 100 bytes for each article, the history file would need to be about 70MB.

When planning disk usage on a Usenet server, it’s always better to have too much than not enough, so for the preceding setup, I’d want a system with at least 4GB of disk space just for news use. I’d probably put 3GB toward spool, and the rest toward the news server’s program storage, the history database, and the log files. Keep in mind that Usenet is growing every day, and as it does the traffic increases. This increase in traffic means something for you as well: You’ll need more disk space.

I remember reading the announcement that a full newsfeed would no longer fit over a 2400-baud modem. There was some excitement among news admins when that announcement came, but nothing like the dismay felt when it was learned that a full newsfeed would no longer fit over a full T1. It was then that we all saw what kind of unpredictable beast we were trying to tame.

## Bandwidth

This brings me to the second type of capacity you need to consider. How much bandwidth does your site have? I’ve run a limited newsfeed (similar to the one discussed) across a dual-channel ISDN line. It would use all our bandwidth at times, but not usually. If you are limited to ISDN, or a fractional T1, you might want to carry only a partial newsfeed. You definitely won’t want to carry alt.binaries.*. The alt.binaries hierarchy, in my estimations, accounts for more than 60% of the Usenet bulk. There may not be as many articles posted in these groups as in the rest, but they are much larger on average because many of them include encoded binary files (pictures, fonts, sounds, and so on).

There are really two types of newsfeeds: full feeds and interest-based feeds. I’d suggest that unless you want to become a major hub in Usenet, you start with an interest-based feed. Figure out what your users want and give it to them. Start with a small feed as outlined previously and add groups as requested. A full newsfeed actually won’t fit across two T1 lines anymore. One hundred percent of a T1 is about 16GB of traffic a day. You never really get 100% of your bandwidth, so if you assume 75%, you can get about 12GB of news each day. Don’t forget about your outgoing newsfeeds and your user traffic. Now you’re down to about 10GB each day on a T1. For a full newsfeed, you would need three T1 lines to just barely keep up. If you really want a full newsfeed, you may want to consider co-locating your server somewhere upstream from your Internet site.

## Running a News Server

Usenet is very unpredictable. It might even be considered alive. It consumes (disk), it reproduces (you’re thinking about starting a server, or you wouldn’t still be reading this chapter), it grows (at an exponential rate), and it repairs itself (you, you repair it when your server goes down, but then you’re a part of it also). The biggest problem you are going to have with a news server is that it is very hungry. It will use a lot of disk space. Once you get a server up and running and accepting a feed from a peer, your daily maintenance consists mainly of watching disk space. To keep your available space in check, you’ll find that you’re constantly adjusting the amount of time before old articles are deleted (your expire times). You’ll want to start with fairly short expire times (a few days) and expand as your disks allow. Then just when you think you’ve got it right, along comes a surge in traffic and you’ll have to back your expire times down some.

The daily reports that come from the nightly maintenance program contain a lot of information. You should pay attention to disk space and your incoming and outgoing traffic. If you find that you are suddenly not sending any articles to any of your peers, or you aren’t accepting any articles from any of them, you might have a problem. If you find that your disk space is filling up rapidly and nothing seems to be expiring, you most definitely have a problem. Disk space is your biggest worry. Other than disk space problems, your readers will bring most other problems with the news server to your attention. Things such as no new articles coming in or no outgoing posts will probably be brought to your attention before you notice them in your daily reports. Next to disk space and traffic problems, you’ll have a lot of mail to read because of your Usenet server. It all gets sent to news or usenet@your.domain. You’ll want to add those aliases to your mail configuration. Refer to Chapter 20, “Electronic Mail,” for more information on that. Other problems are related to the specific news server software (which we’ll discuss later), or hardware failure, which we can’t do anything about.
