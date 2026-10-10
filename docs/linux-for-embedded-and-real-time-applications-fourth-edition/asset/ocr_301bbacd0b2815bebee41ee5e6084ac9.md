In the case of GET, the function `doGetMethod()` near line 183 opens the specified file, and determines its content type. In “real” web servers like Apache, HTML files are kept in a specific directory. In this case it just seems easier to put the files in the same directory as the program, so `doGetMethod()` strips off the leading “/” if present, to make the path relative to the current directory.

If everything is OK, we call `responseHeader()` to send the success response. The response header indicates the content type of the file, and also tells the server that we want to close the connection, even if the client asked to keep the connection alive. Finally, we send the file itself. If it is an HTML file, we need to parse it looking for dynamic content tags.

# **Dynamic Web Content**

Just serving up static HTML web pages is not particularly interesting, or even useful, in embedded applications. Usually, the device needs to report some information and we may want to exercise some degree of control over it. There are a number of ways to incorporate dynamic content into HTML, but, since this is not a book on web programming, we are going to take a “quick and dirty” approach.

This is a good time to do a quick review of HTML. Take a look at the file `index.html` in the network/ directory.

A nice feature of HTML is that it is easily extensible. You can invent your own tags. Of course, any tag the client browser does not understand it will simply ignore. So if we invent a tag, it has to be interpreted by the server before sending the file out. We’ll invent a tag called <DATA> that looks like this:

```
<DATA data_function>
```

`index.html` has one data tag in it.

The server scans the HTML text looking for a <DATA> tag. `data_function` is a function that returns a string. The server replaces the <DATA> tag with the returned string. Open `webvars.c`. Near the top is a table with two entries each consisting of a text string and a function name. Just below that is the function `cur_temp()`, which returns the current temperature of our thermometer as an ASCII string.

Now go back to `webserver.c`, and find the function `parseHTML()` around line 124. It scans the input file for the <DATA> tag. When one is found, it writes everything up to the tag out to the socket. Then it calls `web_var()` with the name of the associated data function. `web_var()`, in `webvars.c`, looks up and invokes the data function, and returns its string value. The return value from `web_var()` is then written out and the scan continues.