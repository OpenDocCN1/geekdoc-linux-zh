# Linux Web Server Toolkit

> TIP If you need faster performance, write your cgi-bin programs in compiled C. If you need something a little less obtuse, use a BASIC variant. The principles in this section apply in any case.

# ## Choosing a Method

Data from the Web browser can be sent to the Web server in one of two ways: GET or POST. You specify which method to use by what you enter in the METHOD option of the FORM tag.

# ## USING THE GET METHOD

The GET method sends all data as part of the URL.
The name of the script that processes the data is followed by a question mark. Then each name-value pair is tacked onto the end of the URL, each pair being separated by an ampersand (&). Spaces are converted to plus signs (+), and any non-alphanumeric characters are represented by their hexadecimal values preceded by a percentage sign — for example, a space can also be represented by %20 because a space has a decimal value of 32, which is 20 in hexadecimal.

A form that uses the GET method to send data to the query.pl script (.pl is the extension for a Perl script file) might use a beginning FORM tag like the following:

```
<FORM ACTION= http://www.hondaclub.org/cgi-bin/query.pl METHOD= GET model=accord&year=1993&color=blue
```

If the form included three fields, to generate three name-value data pieces for the script, the URL sent back to the Web server when the user pressed the Submit button might look like the following:

```
http://www.hondaclub.org/cgi-bin/
query.pl?model=accord&year=1993&color=blue
```

The query.pl script can read the value of the QUERY_STRING environment variable and separate each of the variables that were submitted with the URL. That's one reason to use Perl; it can separate the entire query string into an ordered array of values with a single command.

> TIP If your forms have a lot of data, GET doesn't work well because the total length of a URL often can't exceed 256 characters.