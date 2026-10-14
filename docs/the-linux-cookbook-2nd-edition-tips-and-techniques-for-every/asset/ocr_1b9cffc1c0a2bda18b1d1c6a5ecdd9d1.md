smaller and faster to use than a browser, and it shows a visual display of the download progress.

To retrieve an HTML file from the Web and save it as rendered text, use Lynx instead—see Recipe 33.2.4 [Sending Text from the Web to Standard Output], page 646.

The following subsections contain recipes for using wget to retrieve information from the Web. For more examples of things you can do with wget, consult its Info documentation (see Recipe 2.8.5 [Reading an Info Manual], page 48).

# 33.5.1 Downloading an URL

To download a single file from the Web, give the URL of the file as an argument to wget.

⇒ To download ftp://garbo.uwasa.fi/garbo-gifs/garbo20.gif to a file, type:

```
$ wget ftp://garbo.uwasa.fi/garbo-gifs/garbo20.gif [RET]
```

This command downloads a given URL, writing to a file in the current working directory with the same name as the original URL, garbo20.gif.

If you interrupt a download before it’s finished, the contents of the file you were retrieving will contain only the portion of the file wget retrieved before it was interrupted. Use wget with the -c option to resume the download from the point it left off.

⇒ To resume a download of the URL from the previous example, type:

```
$ wget -c ftp://garbo.uwasa.fi/garbo-gifs/garbo20.gif [RET]
```

NOTES: In order for the -c option to have the desired effect, you should run wget from the same directory as it was run previously, where that partially-retrieved file should still exist.

# 33.5.2 Archiving an Entire Web Site

To archive a single Web site, use wget with the -m ("mirror") option, which saves files with the exact timestamp of the original, if possible, and sets the "recursive retrieval" option to download everything. To specify the number of retries to use when an error occurs in retrieval, use the -t option with a numeric argument—t3 is usually good for safely retrieving across the net; use -t0 to specify an infinite number of retries, good for when a network connection is really bad but you really want to archive something, regardless