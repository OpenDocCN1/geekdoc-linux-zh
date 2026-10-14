```
{
  "args": {},
  "headers": {
    "Accept": "*/*",
    "Connection": "close",
    "Host": "httpbin.org",
    "User-Agent": "curl/7.47.0"
  },
  "origin": "459.203.134.88",
  "url": "http://httpbin.org/get"
}
```

The text that we get back from the request specifies four information groups: args, headers, origin, and url. The origin shows our own IP address, and url shows where we sent the request. The headers group shows some interesting information, including the User-Agent which shows that httpbin.org knows that we sent this request with curl. Notice that the args group is empty. The args group is short for arguments, which hints at the fact that we can provide arguments in an HTTP request, just like arguments we would use for a function, or the arguments we used in the GitHub API.

In the general case we can provide arguments to an HTTP API by putting a question mark (?) after the API's URL. Let's try this out:

```
curl http://httpbin.org/get?Baltimore
```