# #63 Seeing the CGI Environment

While we were developing some of the scripts for this chapter, Apple released the latest version of its Safari web browser. Our immediate question was, "How does Safari identify itself within the HTTP_USER_AGENT string?" Finding the answer is simple for a CGI script written in the shell, as in Listing 8-3.

# The Code

```
#!/bin/bash

# showCGIenv--Displays the CGI runtime environment, as given to any
# CGI script on this system
echo "Content-type: text/html"
echo ""

# Now the real information...

echo "<html><body bgcolor=\"white\"><h2>CGI Runtime Environment</h2>"
echo "<pre>"
env || printenv
echo "</pre>"
echo "<h3>Input stream is:</h3>"
echo "<pre>"
cat -
echo "(end of input stream)</pre></body></html>"

exit 0
```

Listing 8-3: The showCGIenv script

# How It Works

When a query comes from a web client to a web server, the query sequence includes a number of environment variables that the web server (Apache, in this instance) hands to the script or program specified (the CGI). This script displays this data by using the shell env command —to be maximally portable, it’ll use printenv if the env invocation fails, the purpose of the | notation—and the rest of the script is necessary wrapper information to have the results fed back through the web server to the remote browser.

# Running the Script

To run the code you need to have the script executable located on your web server. (See "Running the Scripts in This Chapter" on page 201 for more details.) Then simply request the saved .cgi file from within a web browser. The results are shown in Figure 8-1.