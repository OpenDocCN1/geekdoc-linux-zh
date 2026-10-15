everything after the "References" string in the web page text **5**. Then the script processes the list of links as needed based on the user-specified flags.

One interesting technique demonstrated by this script is the way the variable lastcmd (**1, 2, 3, 4**) is set to filter the list of links that it extracts according to the flags specified by the user. Once lastcmd is set, the amazingly handy eval command **6** is used to force the shell to interpret the content of the variable as if it were a command instead of a variable.

# Running the Script

By default, this script outputs a list of all links found on the specified web page, not just those that are prefaced with http: . There are three optional command flags that can be specified to change the results, however: -d produces just the domain names of all matching URLs, -r produces a list of just the *relative* references (that is, those references that are found on the same server as the current page), and -a produces just the *absolute* references (those URLs that point to a different server).

# The Results

A simple request is a list of all links on a specified website home page, as Listing 7-5 shows.

```
$ getlinks http://www.daveonfilm.com/ | head -10
http://instagram.com/d1taylor
http://pinterest.com/d1taylor/
http://plus.google.com/110193533410016731852
https://plus.google.com/u/0/110193533410016731852
https://twitter.com/DaveTaylor
http://www.amazon.com/Doctor-Who-Shada-Adventures-Douglas/
http://www.daveonfilm.com/
http://www.daveonfilm.com/about-me/
http://www.daveonfilm.com/author/d1taylor/
http://www.daveonfilm.com/category/film-movie-reviews/
```

Listing 7-5: Running the getlinks script

Another possibility is to request a list of all domain names referenced at a specific site. This time, let’s first use the standard Unix tool wc to check how many links are found overall:

```
$ getlinks http://www.amazon.com/ | wc -l
219
```

Amazon has 219 links on its home page. Impressive! How many different domains does that represent? Let’s generate a list with the -d flag:

```
$ getlinks -d http://www.amazon.com/ | head -10
amazonlocal.com
aws.amazon.com
fresh.amazon.com
kdp.amazon.com
```