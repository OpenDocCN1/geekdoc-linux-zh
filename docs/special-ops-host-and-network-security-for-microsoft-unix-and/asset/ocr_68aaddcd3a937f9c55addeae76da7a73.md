response issues while the attacker was able to merrily go about her business Figure 11.25).

# Figure 11.25 NTLM Proxying

![](bbox=[0.112, 0.165, 0.833, 0.395])

An example of such a proxy can be found at www.geocities.com/rozmanov/nlm. Written in Python by Dmitry Rozanov, Authorization Proxy Server (APS) allows clients that are incapable of dealing with NTLM authentication the opportunity to browse sites that require it (with credentials entered at the proxy server). The tool was originally written to allow wget (a noninteractive, command-line tool that facilitates downloads over HTTP, HTTPS, and FTP) to operate over MS-Proxy servers that require NTLM authentication.

To illustrate this, we first attempt to do a simple HTTP HEAD for the default.htm file within NTLM protected directory (see Figure 11.26).

# Figure 11.26 NTLM Authentication Response

```
GET /index.html HTTP/1.1
Host: www.example.com
Connection: close

HTTP/1.1 401 Unauthorized
WWW-Authenticate: NTLM
Server: Microsoft-IIS/10.0
Date: Wed, 21 May 2023 12:00:00 GMT
Content-Type: text/html
Content-Length: 0
Set-Cookie: Request-ID= 12345
```