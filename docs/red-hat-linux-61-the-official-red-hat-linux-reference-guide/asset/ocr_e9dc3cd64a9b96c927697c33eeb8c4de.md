# Chapter 10. Apache HTTP Server

ErrorHandler cgi-script .cgi

This directive enables CGIs outside of the cgi-bin to function in any directory on the server which has the ExecCGI option within the directories container. Refer to Section 10.5.24 Directory for more information about setting the ExecCGI option for a directory.

In addition to cgi scripts, the AddHandler directive is used to process server-parsed HTML and image-map files.

# ## 10.5.60. Action

Action specifies a MIME type and CGI script pair, whenever a file of media type is requested, a particular CGI script is executed.

# ## 10.5.61. ErrorDocument

The ErrorDocument associates an HTTP response code with a message or a URL to be sent back to the client. By default, the Web server outputs a simple and usually cryptic message when an error occurs. The ErrorDocument directs the Web server to output a customized message or redirects the client to a local or external URL.

> **Important**

In order to be valid, the message must be enclosed in a pair of double quotes "".

# ## 10.5.62. BrowserMatch

The BrowserMatch allows the server to define environment variables and take appropriate actions based on the User-Agent HTTP header field — which identifies the client's browser type. By default, the Web server uses BrowserMatch to deny connections to specific browsers with known problems and also to disable keepalives and HTTP headers for browsers that are known to have problems with those actions.

# ## 10.5.63. Location

The <Location> and </Location> tags create a container in which access control based on URL can be specified.

For instance, to allow people connecting from the server's domain to see status reports, use the following directives:

```
<Location /server-status>
SetHandler server-status
Order deny,allow Deny from all
Allow from <.example.com>
</Location>
```

Replace <.example.com> with the second-level domain name for the Web server.

To provide server configuration reports (including installed modules and configuration directives) to requests from inside the domain, use the following directives: