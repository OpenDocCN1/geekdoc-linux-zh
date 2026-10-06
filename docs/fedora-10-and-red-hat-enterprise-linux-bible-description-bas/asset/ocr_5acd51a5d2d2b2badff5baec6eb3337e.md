# Chapter 21: Setting Up a Web Server 875

DELETE). These options allow scripts to be executed whenever a file of the appropriate MIME type is requested, a handler is called, or a request method is invoked.

# Customizing error responses

For different error conditions that occur, you can define specific responses. The responses can be in plain text, redirects to the local server, or redirects to external pages:

```
#
# Customizable error responses come in three flavors:
# 1) plain text 2) local redirects 3) external redirects
#
# Some examples:
#ErrorDocument 500 "The server made a boo."
#ErrorDocument 404 /missing.html
#ErrorDocument 404 /cgi-bin/binding/missing_handler.pl
#ErrorDocument 402 http://www.example.com/subscription_info.html
```

As the comments suggest, the ErrorDocument directive can customize any server response, redirecting it to an external page, a local file or CGI script, or to a simple text sentence. Table 21-6 lists the most common server response codes and their meanings.

# Table 21-6: HTTP Response Codes

| Response Code | Meaning |
|---|---|n| 200 OK | The request was successfully processed. |
| 201 Created | Using the POST request method, a new file was successfully created on the server. |
| 202 Accepted | The request has been received and is currently being processed. |
| 204 No Content | The request was successful, but there is no change in the current page displayed to the client. |
| 301 Moved Permanently | The requested page has been permanently moved, and future references to that page should use the new URL that is displayed. |
| 302 Moved Temporarily | The requested page has been temporarily relocated. Future references should continue to use the same URL, but the current connection is being redirected. |
| 304 Not Modified | A cached version of the page is identical to the requested page. |
| 400 Bad Request | The client's request contains invalid syntax. |
| 401 Unauthorized | The client specified an invalid username/password combination. |
| 402 Payment Required | The client must provide a means to complete a monetary transaction. |
| 403 Forbidden | Access-control mechanisms deny the client's request. |