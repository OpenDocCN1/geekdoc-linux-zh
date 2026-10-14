The data presented on this site comes from daily scrapes of the broadcasters’ own web sites, along with traditional data feeds, so it is accurate and timely. It is also legal, as permission has been granted to the site for its inclusion.

> **Note**  Curiously, the data for the UK’s ITV companies are not available. This includes ITV, ITV2, ITV3, and ITV4. This is because ITV doesn’t want its data shared on other web sites, although it has no objection to using other TV schedule data on its own site! This might be because of the purely commercial aspect of its business. However, until ITV changes its rules (or the petition takes effect), no geek following these instructions will be able to determine what’s on ITV, which in turn will limit ITV’s advertising revenues, causing them to have shot themselves in the proverbial foot!

The data itself is available as a web page on the site or as XML files that can be downloaded to your PC and processed at your leisure. The URLs for each XML file follow a strict format so that you can automate the process.

The root URL is http://www.bleb.org/tv/data/listings and is followed by this:

+   - The day offset, between -1 (yesterday) and 6 (next week)
+   - The station name

Therefore, you can find today’s BBC1 schedule here:

http://www.bleb.org/tv/data/listings/0/bbc1.xml

And tomorrow’s TMF guide is here:

http://www.bleb.org/tv/data/listings/1/tmf.xml

The format is XMLTV and very easy to parse with a suitable library or even XSLT. With this data in a local usable format, you can then search the descriptions for films starring your favorite actors, be alerted to new series, or check for musicians appearing within talk shows or programs outside your usual sphere. These results can be piped into any file, such as a web page or e-mail, for review.

Despite its free nature, Bleb does have a couple of restrictions of its own, but the only requirements are that you don’t repeatedly ask for data from the server by including a two-second gap between requests and that you include the program name that’s making these requests along with an e-mail.

Minerva includes an example of this in action; I cover this in Chapter 7. There are many other examples, such as executables for Windows, Flash code, and the WhenIsItOn code found here:

http://cgi.useyourhead.force9.co.uk/

This alphabetically sorts the entire week’s TV schedule so that you can see at what time the show is on and when it’s repeated.

# Train Times

Like the TV schedules, obtaining complete timetables for every train around the world is a thankless and impossible task. But fortunately, like TV, the rail journeys of interest are generally based in one country, so you need to find only one suitable data source for your area.

Any search engine will return several different data sources for this information, depending on your country, so you need to spend a little time looking at each one to determine which have APIs (that are usable) or, failing that, which can be scraped with the least amount of effort. Most people who use trains regularly have a routine, and they