If a token does not have a value, then it is represented by a hyphen (-). Tokens have the following meanings:

+   - **host** — The fully qualified domain name of the client, or its IP address.
+   - **ident** — If the IdentityCheck directive is enabled and the client machine runs identd, then this is the identity information reported by the client.
+   - **authuser** — If the requested URL required a successful Basic HTTP authentication, then the user name is the value of this token.
+   - **date** — The date and time of the request.
+   - **request** — The request line from the client, enclosed in double quotes (").
+   - **status** — The three-digit HTTP status code returned to the client.
+   - **bytes** — The number of bytes in the object returned to the client, excluding all HTTP headers.

![](bbox=[0.08, 0.6, 0.16, 0.68])

See Appendix B for a list of all HTTP/1.1 status codes.

The date field can have the following format:

```
date = [day/month/year:hour:minute:second zone]
```

For example:

```
[03/Jul/2001:00:22:01 -0800]
```

The field sizes are given in Table 12-6.

# Table 12-6 Date Field Sizes

| Fields | Value |
|---|---|
| day | 2 digits |
| month | 3 letters |
| year | 4 digits |
| hour | 2 digits |