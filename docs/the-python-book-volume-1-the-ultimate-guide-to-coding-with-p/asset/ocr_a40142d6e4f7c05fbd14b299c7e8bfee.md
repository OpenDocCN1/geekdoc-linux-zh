```
import os, sys, urllib2, argparse, datetime, exit
from bs4 import BeautifulSoup

addresses = []
deepestAddresses = []

maxLevel = 3
storeFolder = "WikiStore"

undesirables = [ {"element": "table", "attr": {"class": "infobox"}}, {"element": "table", "attr": {"class": "vertical-navbox"}}, {"element": "span", "attr": {"class": "mw-editsection"}}, {"element": "div", "attr": {"class": "thumb"}}, {"element": "sup", "attr": {"class": "reference"}}, {"element": "div", "attr": {"class": "mw-parser-output"}}, {"element": "table", "attr": {"class": "nowraplinks"}}, {"element": "a", "attr": {"class": "mw-redirect"}}, {"element": "script", "attr": {"type": "text/javascript"}}, {"element": "table", "attr": {"class": "box-small"}}, {"element": "span", "attr": {"id": "coordinates"}}, {"element": "table", "attr": {"class": "mbox-small"}}, {"element": "div", "attr": {"class": "hatnote"}}, {"element": "span", "attr": {"id": "References"}} ]
global maxLevel

def init():
    parser = argparse.ArgumentParser(description="Handle the starting page and number of levels we're going to scrape")
    parser.add_argument("--URL", dest="link", action="store", help="The Wikipedia page from which we will start scraping")
    parser.add_argument("--levels", dest="levels", action="store", help="How many levels deep should the scraping go")
    args = parser.parse_args()
    if(args.levels != None):
        maxLevel = int(args.levels)
    if(args.link != None):
        print("You need to pass a link with the -URL flag")
        sys.exit(0)
    else:
        if not os.path.exists(storeFolder):
            os.makedirs(storeFolder)
        grabPage(args.link, 0, args.link.split("/wiki/")[1].strip().replace(":", "_"))
    atexit.register(clenup)

def isValidLink(link):
    if "wiki:" in link and "?" not in link and "http://" not in link and "wikibooks" not in link and "#" not in link and "wikipedia" not in link and "wikitionary" not in link and "wiktionary" not in link and "wikivoyage" not in link and "wikisource" not in link and "wikinews" not in link and "wikiversity" not in link and "wikidata" not in link:
        return True
    else:
        return False
```

> WIKI-EVERYTHING
> Wikipedia has so many different services that interlink with each other; however, we don't want to grab those pages, so we've got quite a lengthy conditional statement to stop that. It's pretty good at making sure we only get links from Wikipedia.

> INFINITE LINKS
> Wikipedia has a lot of links and when you start following links to links to links, the number of pages you have to parse can grow exponentially, depending on the subject matter. By passing through the levels value, we put a cap on the amount of pages we can grab— although the number of files stored can still vary greatly. Use it wisely.

# 01 Install Beautiful Soup & HTML5Lib

Before we can start writing code, we need to install the libraries we'll be using for the program (Beautiful Soup, HTML5Lib, Six). The installation process is fairly standard: grab the libraries from their respective links, then unzip them. In the terminal, enter the unzipped directory and run setup.py install for each library. They will now be ready for use.

# 02 Creating some useful variables

These variables will keep track of the links we've accessed while the script has been running: addresses is a list containing every link we've accessed; deepestAddresses are the links of the pages that were the furthest down the link tree from our starting point; storeFolder is where we will save the HTML files we create and maxLevel is the maximum depth that we can follow the links to from our starting page.

# 03 Handling the user's input

In the first few lines of this function, we're just creating a helper statement. Afterwards, we're parsing any arguments passed into the program on its execution and looking for a -URL flag and a -levels flag. The -levels flag is optional as we already have a preset depth that we'll follow the links to, but we need a link to start from so if the -URL flag is missing, we'll prompt the user and exit. If we have a link, then we quickly check whether or not we have a directory to store files in — which we'll create if we don't — and then we'll fire off the function to get that page. Finally, we register a handler for when the script tries to exit. We'll get to that bit later.

# 04 Retrieving the page from the URL

Here we're using URLLib2 to request the page the the user has asked for and then, once we've received that page, we're going to pass the content through to Beautiful Soup with the soup variable. This gives us access to the methods we're going to call as we parse the document.

# 05 Trimming the fat

Wikipedia has a lot of nodes that we don't want to parse. The content variable allows us to straight away ignore most of Wikipedia's GUI, but there are still lots of elements that we don't want to parse. We remedy this by iterating through the list 'undesirables' that we created

> "Wikipedia has a lot of nodes"