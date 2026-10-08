# Work with Python

# Scrape Wikipedia with Beautiful Soup

# What you'll need...

+   Beautiful Soup
www.crummy.com/software/
BeautifulSoup/
HTML5Slib
https://github.com/html5slib/
html5slib-python
Python 2.6 & WikiParser.
zip Six
https://pypi.org/pypi/six/

# Scrape Wikipedia with Beautiful Soup

Use the Beautiful Soup Python library to parse Wikipedia's HTML and store it for offline reading

In this tutorial we'll use the popular Beautiful Soup to scrape Wikipedia for links to articles and save those pages for offline reading. This is ideal for travelling or in a location with a poor internet connection.

+   The plan is simple: using Beautiful Soup with the HTML5Slib Parser, we're going to load a Wikipedia page, remove all of the GUI and unrelated content, search the content for links to other Wikipedia articles and then, a tiny bit of modification, write them to a file.

Even though it is now the de facto base of the world, Wikipedia isn't great when it comes to DOM consistency – that is, IDs and classes are sometimes quite loose in their usage. Because of this, we will also cover how to handle all of the excess bits and bobs of the Wikipedia GUI that we don't need, as we will use us to find the CSS sheets and a Python scriptertaining to this tutorial at http://bit.ly/19MibbX.

# Infinite Links

Wikipedia has a lot of links and when you start following links to links, the number of pages you have to parse can grow exponentially, depending on the subject matter. By passing them we avoid having a cap on the amount of pages we can grab– although the number of files stored can still vary. Use it wisely.

# Install Beautiful Soup & HTML5Slib

01 Before we start writing code, we need to install the libraries we'll be using for the program (Beautiful Soup, HTML5Slib, Six). The installation process is fairly standard: grab the libraries from their respective links, un them to the terminal, enter the unzipped directory and run setup.py install for each library. They will be ready for use.

> “Wikipedia isn't great when it comes to DOM consistency”

![](bbox=[0.293, 0.923, 0.313, 0.993])