# RESPONSE Object Attributes (continued)

| Name | Explanation |
| --- | --- |
| setCookie(name, value,...) | Causes the response to contain an HTTP-Header that sets up a cookie with the key name and the value "value" on browsers in which cookies are activated, thus overwriting all previously set values for the cookie in the response object. Additional cookie parameters can be inserted by specifying the keyword parameters expires, domain, path, max_age, comment, and secure. |
| getHeader(name) | Returns the value associated with a HTTP-Return-Header or None if such header was set in the response. |
| appendHeader(name, value) | Adds value to http response header, name. If a header by the specified name already exists, the value is appended to the existing header, preceded by comma. |
| redirect(location) | Redirects to another URL without resulting in an error. |

# HTTP Status Codes

| Status as String | Status as Integer |
| --- | --- |
| OK | 200 |
| Accepted | 202 |
| MovedPermanently | 301 |
| MovedTemporarily | 302 |
| NotModified | 304 |
| BadRequest | 400 |
| Unauthorized | 401 |
| Forbidden | 403 |
| NotFound | 404 |
| InternalError | 500 |
| NotImplemented | 501 |
| BadGateway | 502 |
| ServiceUnavailable | 503 |