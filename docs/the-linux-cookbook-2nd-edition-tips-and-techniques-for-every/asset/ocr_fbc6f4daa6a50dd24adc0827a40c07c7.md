Use the -A option to specify the exact file name extensions to accept—for example, use -A txt,tex,tex to only download files whose names end with .txt, .text, and .tex extensions. The -R option works similarly, but specifies the file extensions to reject and not download.

⇒ To download only the files ending in a .gz extension and only in the given directory /~jim/papers/ at example.org, type (all on one line):

```
$ wget -m -r -l1 --no-parent -A.gz
http://www.example.org/~jim/papers/ [RET]
```

# 33.5.4 Reading the Headers of a Web Page

All Web servers output special headers at the beginning of page requests, but you normally don’t see them when you retrieve a URL with a Web browser. These headers contain information such as the current system date of the Web server host and the name and version of the Web server and operating system software.

Use the -S option with wget to output these headers when retrieving files; headers are output to standard output, or to the log file, if used.

⇒ To retrieve the file at http://google.com/ and output the headers, type:

```
$ wget -S http://google.com/ [RET]
```

This command writes the server response headers to standard output and saves the contents of http://google.com/ to a file in the current directory whose name is the same as the original file.

# 33.6 Keeping a Browser History

```
browser-history
DEB: browser-history
RPM: browser-history
WWW: http://www.inria.fr/koala/colas/browser-history/
```

Many Web browsers have a “history” function that keeps a listing of the sites you visit, and the time and date of your visit, but none are as good as the browser-history tool. If you presently keep a weblog (or “blog”) in order to remember good links you find, you won’t have to do that anymore, once you install this tool.

Use browser-history to maintain a history log of all the Web sites you visit.