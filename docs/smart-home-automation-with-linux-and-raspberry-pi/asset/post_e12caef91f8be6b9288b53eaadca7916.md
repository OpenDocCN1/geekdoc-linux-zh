
and the disc’s ID and name:

```bash
DISC_ID=`echo $TITLE | cut -d ' ' -f 3`
DISC_TITLE=`echo $TITLE | cut -d ' ' -f 4-`
```

Using the disc ID and genre, you can determine a unique track listing (since the genre is used to distinguish between collisions in hash numbers) for the disc in question, which allows you to retrieve a parsable list of tracks with this:

```bash
cddb-tool read http://freedb.freedb.org/~cddb/cddb.cgi 6 $(app) $(host) $GENRE $DISC_ID
```

The disc title, year, and true genre are also available from this output.[^8]

A more complex form of data to retrieve is that of the album’s cover art. This is something that rippers, especially text-based ones, don’t do and is something of a hit-and-miss affair in the open source world. This is, again, because of the lack of available data sources. Apple owns a music store, where the covers are used to sell the music and are downloaded with the purchase of the album. If you rip the music yourself, you have no such option.

One graphical tool that can help here is albumart. You can download this package from [www.unrealvoodoo.org/hiteck/projects/albumart](http://www.unrealvoodoo.org/hiteck/projects/albumart) and install it with the following:

```bash
dpkg -i albumart_1.6.6-1_all.deb
```

This uses the ID tags inside the MP3 file to perform a search on various web sites, such as [Buy.com](http://Buy.com), [Walmart.com](http://Walmart.com), and Yahoo! The method is little more than screen scraping, but provided the files are reasonably well named, the results are good enough and include very few false positives. When it has a problem determining the correct image, however, it errs on the side of caution and assigns nothing, waiting for you to manually click Set as Cover, which can take some time to correct. Once it has grabbed the art files, it names them folder.jpg in the appropriate directory, where it is picked up and used by most operating systems and media players. As a bonus, however, because the album art package uses the ID tags from the file, not the CD fingerprint, it can be used to find images for music that you’ve already ripped.

> **Note** Unlike track listings, the cover art is still copyrighted material, so no independent developer has attempted to streamline this process with their own database.

Correctly finding album covers without any IDs or metadata can be incredibly hard work. There is a two-stage process available should this occur. The first part involves the determination of tags by looking at the audio properties of a song to determine the title and the artist. MusicBrainz is the major (free) contender in this field. Then, once you have an ID tag, you can retrieve the image as normal. These steps have been combined in software like Jaikoz, which also functions as a mass-metadata editing package that may be of use to those who have already ripped your music, without such data.

## News

Any data that changes is new, and therefore news, making it an ideal candidate for real-time access. Making a personalized news channel is something most aggregators are doing through the use of RSS feeds and custom widgets. The soon to be retired iGoogle (www.google.com/ig), for example, also includes integration with its Google Mail and Calendar services, making this a disturbingly useful home page when viewed as a home page, but its enclosed nature makes it difficult to utilize this as a data input for a home. Instead, I’ll cover methods to retrieve typical news items as individual data elements, which can be incorporated in a manner befitting ourselves. This splits into two types: push and pull.

### Reported Stories: Push

The introduction of push-based media can be traced either to 24-hour rolling news (by Arthur W. Arundel in 1961) or to RSS feeds, depending on your circumstances. Both formats appear to push the information in real time, as soon as it’s received, to the viewer. In reality, both work by having the viewer continually pull data from the stream, silently ignoring anything that hasn’t changed. In the case of TV, each pull consists of a new image and occurs several times a second. RSS happens significantly less frequently but is the one of interest here.

### RSS Feeds

RSS[^1] is an XML-based file format for metadata. It describes a number of pieces of information that are updated frequently. This might include the reference to a blog post, the next train to leave platform 9¾ from King’s Cross, the current stories on a news web site, and so on. In each case, every change is recorded in the RSS file, along with the all-important time stamp, enabling RSS readers to determine any updates to the data mentioned within it. The software that generates these RSS feeds may also remove references to previous stories once they become irrelevant or too old. However, old is defined by the author.

This de facto standard allows you to use common libraries to parse the RSS feeds and extract the information quite simply. One such library is the PHP-based MagpieRSS (http://magpierss.sourceforge.net), which also supports an alternative to RSS called Atom feeds and incorporates a data cache. This second feature makes your code simpler as you can re-use all the data from the RSS feed, without a concern for the most recent, because the library has cached the older stories automatically.

You utilize MagpieRSS in PHP by beginning with the usual code:

```php
require_once 'rss_fetch.inc';
```

Then you request a feed from a given URL:

```php
$rss = fetch_rss($url);
```

Naturally, this URL must reference an RSS file (such as www.thebeercrate.com/rss_feed.xml) and not the page that it describes (which would be www.thebeercrate.com). It is usually indicated by an orange button with white radio waves or simply an icon stating “RSS-XML.” In all cases, the RSS file appears on the same page whose data you want to read. You can then process the stories with a simple loop such as the following:

```php
$maxItems = 10;
$lastItem = count($rss->items);

if ($lastItem > $maxItems) {
    $lastItem = $maxItems;
}

for($i=0;$i < $maxItems;++$i) { /* process items here */ }
```

As new stories are added, they do so at the beginning of the file. Should you want to capture everything, it is consequently important to start at the end of the item list, as they will disappear sooner from the feed.

As mentioned earlier, the RSS contains only metadata, usually the title, description, and link to the full data. You can retrieve these from each item through the data members:

```php
$rss->items[$i]['link'];
$rss->items[$i]['title'];
$rss->items[$i]['description'];
```

They can then be used to build up the information in the manner you want. For example, to recreate the information on your own home page, you would write the following:

```php
$html = "<a href='".$rss->items[$i]['link']."'>".$rss->items[$i]['title']."</a>";
$html .= "<p>".$rss->items[$i]['description']."</p>";
```

Or you could use a speech synthesizer to read each title:

```php
system("say default "+$rss->items[$i]['description']);
```

You can then use an Arduino that responds to sudden noises such as a clap or hand waving by a sensor (using a potential divider circuit from Chapter 2, with a microphone and LDR, respectively) to trigger the full story.

You can also add further logic, so if the story’s title includes particular key words, such as NASA, you can send the information directly to your phone.

```php
if (stristr($rss->items[$i]['title'], "nasa"))
    system("sendsms myphone "+$rss->items[$i]['description']);
```

This can be particularly useful for receiving up-to-minute sports results, lottery numbers, or voting information from the glut of reality TV shows still doing the rounds the world over. Even if it requires a little intelligent pruning to reduce the pertinent information into 140 octets (in the United States) or 160 characters (in Europe, Asia, and Oceania), which is the maximum length of a single unconcatenated text message, it will be generally cheaper than signing up for the paid-for services that provide the same results.

### Retrieving Data: Pull

This encompasses any data that is purposefully requested when it is needed. One typical example is the weather or financial information that you might present at the end of the news bulletin. In these cases, although the information can be kept up-to-date in real time by simulating a push technology, few people need this level of granularity—once a day is enough. For this example, you will use the data retrieved from an online API to produce your own currency reports. This can be later extended to generate currency conversion tables to aid your holiday financing since home automation, as we’ve seen, doesn’t stop at the front door. Even when you’re abroad, you can make use of public data sources to keep a check on your spending by performing currency conversion.

[^8]: There is one main unsolved problem with this approach. That is, if there are two discs with the same fingerprint or two database entries for the same disc, it is impossible to automatically pick the correct one. Consequently, a human needs to untangle the mess by selecting one of the options.

[^1]: RSS currently stands for Really Simple Syndication, but its long and interesting history means that it wasn’t always so simple.
