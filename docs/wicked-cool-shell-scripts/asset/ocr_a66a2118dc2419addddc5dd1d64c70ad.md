# How It Works

The most notable elements of the script have to do with how web servers and web clients communicate. The information entered into the search box is sent to the server as the variable QUERY_STRING, encoded by replacing spaces with the + sign and other non-alphanumeric characters with the appropriate character sequences. Then, when the search pattern is logged, all + signs are translated back into spaces safely and simply. Otherwise the search pattern is not decoded, to protect against any tricky hacks a user might attempt. (See the introduction to this chapter for more details.)

Once logged, the web browser is redirected to the actual DuckDuckGo search page with the Location: header value. Notice that simply appending ?SQUERY_STRING is sufficient to relay the search pattern to its final destination, however simple or complex the pattern may be.

The log file produced by this script prefixes each query string with the current date and time to build up a data file that not only shows popular searches but can also be analyzed by the time of day, the day of the week, the month, and so forth. There’s lots of information that this script could reveal about a busy site!

# Running the Script

To really use this script, you need to create the HTML form, and you need to have the script executable and located on your server. (See “Running the Scripts in This Chapter” on page 201 for more details.) However, we can test the script by using curl. To test the script, perform an HTTP request with curl that has a q parameter with the search query:

```
$ curl "10.37.129.5/cgi-bin/log-duckduckgo-search.cgi?q=metasploit"
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>302 Found</title>
</head><body>
<h1>Found</h1>
<p>The document has moved <a href="https://duckduckgo.com/
html?q=metasploit">here</a>.</p>
<hr>
<address>Apache/2.4.7 (Ubuntu) Server at 10.37.129.5 Port 80</address>
</body></html>
$
```

Then, verify that the search was logged by printing the contents of our search log to the console screen:

```
$ cat searchlog.txt
Thu Mar 9 17:20:56 CST 2017: metasploit
$
```