# Work with Python

# Scrape Wikipedia with Beautiful Soup

# Wiki-Everything

Wikipedia has so many different services that interlink with each other, we don't want to grab those pages, so we've got a lengthy conditional statement to stop that. It's pretty good at making sure we only get link from Wikipedia.

# Creating useful variables

02 These variables will keep track of the links we've accessed while the script has been running; addresses is a list containing every link we've accessed; deepestAddresses are the links of the pages that were furthest down the link from our starting point; storeFolder is where we will save the HTML files and maxLevel is the maximum depth that we can follow the links to our starting page.

# Handling the user's input

03 In the first few lines of this function, we're just creating a helper statement. Afterwards, we're parsing any arguments passed to the program on execution and looking for a -URL flag and a -levels flag. The -levels flag is optional if we already have a preset depth that'll follow the links to, but we need a link to start from if the -URL flag is missing, we'll prompt the user and exit. If we have a link, then we quickly check whether or not we have a directory to store files in - then we'll create it if we don't - we'll call off the function to get that page. Finally, we register a handler for when the script tries to exit.

# Retrieving the page from the URL

04 Here we're using urllib to request the page the user has asked for and then, once we've received that page, we're going to pass the content through to BeautifulSoup with the soup variable. This gives us access to the methods we're going to call as we parse the document.

# Trimming the fat

05 Wikipedia has a lot of nodes that we don't want to parse. The content allows us to straight away ignore most of Wikipedia's GUI, but there are still lots of elements that we don't want to parse. We remedy this by iterating through the list 'undesirables' that we created earlier in the document. For each different div/section/node that we don't want, we call BeautifulSoup's find_all() method and extract that node from the document. At the end of the undesirables list, most of the content we dont want any will be gone. We also look for the 'also' element in the Wiki page. Generally, everything after this is of use to us. By calling the find_all_next() method on the also node, we can get a list of every element we can remove from that point on.

> "The HTML page uses built-in browser styles when rendering the page"