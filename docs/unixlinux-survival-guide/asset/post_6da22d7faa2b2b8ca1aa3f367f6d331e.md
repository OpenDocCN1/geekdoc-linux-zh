
## 6.2.2.4 Using RSS to Document and Communicate

RSS is a topic that is covered in almost all IT-related publications. It is short for Really Simple Syndication. It is a protocol to publish news and other information in a fast and easy way to many receivers. The idea behind RSS is as follows: news to be published is wrapped into a defined XML format and is thus readable by a variety of programs, so-called News Readers. The simplest action taken by these News Readers is to display the incoming data on the screen. This step requires a minimal amount of processing. It is possible, though, to integrate the incoming information into a publication as well, whether it be into a Web site or on paper. A list of a variety of News Readers for the common operating systems can be found at http://blogs.law.harvard.edu/tech/directory/5/aggregators. There are even News Readers to be used on hand-held computers (PDAs) or mobile phones, provided the device is able to connect to a network in one way or the other. On the other hand, the file can be simply copied to the device, but then the news is just as current as the copy on the device, of course.

Figure 6.1 and Figure 6.2 demonstrate how News Readers display incoming information.

![](img/e121d664a879353483b8ef78e54b87ea_204_0.png)

FIGURE 6.1 A News Reader showing title and description.

![](img/e121d664a879353483b8ef78e54b87ea_205_0.png)

FIGURE 6.2 A News Reader displaying only the title.

The structure used in such a document is quite simple regarding the required XML tags. The examples to follow adhere to RSS 2.0. This specification should be readable by almost all programs in circulation. Listing 6.22 shows the basic structure of an RSS channel.

### LISTING 6.22 RSS Document Structure without Contents

```
<rss version="2.0">
<channel>
<title></title>
<link></link>
<description></description>
...
</channel>
</rss>
```

The structure is, as already mentioned, really simple, hence the name. Enclosed in the <title> tags is the name of the news feed, <link> points to a URL containing the Web site delivering the information, and <description> contains a short description of the type of news originating from that site. The ellipsis marks the spot where the content is supposed to be. The content is called an item, using an equally simple structure; it is shown in Listing 6.23.

### LISTING 6.23 Item Structure RSS 2.0

```
<item>
<title></title>
<description></description>
</item>
```

This is the core structure of a message or a news item, using only the required tags, although it diverts from the original specification just a little. The specification allows you to use just <title> or <description>, but some News Readers cannot

display items without a title. This is the so-called ticker mode, just displaying the titles of the incoming messages. Therefore, you should use both, thus making sure the intended recipients really get the information.

That's enough information based on theory only; Listing 6.24 shows how a complete file could look.

### LISTING 6.24 Complete RSS File Containing Three News Items

```
<rss version="2.0">
<channel>
<title>example.domain internal news</title>
<link>http://internalweb.example.domain/</link>
<description>example.domain internal newswire</description>
<language>en</language>
<item>
<title>New RAID system installation</title>
<link>http://internalweb.example.domain/newraid.html</link>
<description>
The installation of the new RAID system was successful.
The increased storage will be available shortly.
Thank you
</description>
</item>
<item>
<title>The Cluster will upgraded to 1024 CPUs</title>
<link>http://internalweb.example.domain/cpucluster.html</link>
<description>
The SUN cluster will be expanded to 1024 CPUs starting next week.
There are no downtimes expected during the upgrade phase, all
GRID apps should continue running as expected. The increased speed
should help us to achive the set goals regarding the calculations.
Thank you
</description>
</item>
<item>
<title>Backup Schedule changes starting tomorrow</title>
<link>http://internalweb.example.domain/back sched.html</link>
<description>
The backup schedule will be changed starting tomorrow.
The new times to create the snapshots of Oracle instances
"ACC1" and "ANS42" will be moved to 1:30 AM.
Please move Reportgeneration accordingly.
Thank you
</description>
```
