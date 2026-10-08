# Chapter 5: Authentication

![](bbox=[0.14, 0.122, 0.859, 0.335])

Figure 5-1. A web browser prompts a user for Basic authentication credentials.

> NOTE To configure the realm on IIS, the IISAdmin tool, select properties of the Master WWW Service, navigate to Directory Security, and select Anonymous Access | Basic | Edit. This is also configured via the UseHostName value in the IIS Metabase.

Once the user types in his or her password, the browser rerequests, this time with the authentication credentials. Here is what a typical Basic authentication exchange like in raw HTTP (edited for brevity). First, the initial request for a resource secured using Basic authentication:

```
GET /test/secure HTTP/1.0
```

The server responds with an HTTP 401 Unauthorized (authentication required) message containing the WWW-Authenticate: Basic header.

```
HTTP/1.1 401 Unauthorized
WWW-Authenticate: Basic realm="luxor"
```

This pops up a window in the client browser that enters his or her username and password into this window, and clicks OK to send it via HTTP:

```
GET /test/secure HTTP/1.0
Authorization: Basic DGvzDp0ZXXNO
```

Note that the client has essentially just re-sent the request, this time with an Authorization header. The server responds with either another “unauthorized” message if the credentials are incorrect, a redirect to the resource requested, or the resource itself, depending on the server implementation.