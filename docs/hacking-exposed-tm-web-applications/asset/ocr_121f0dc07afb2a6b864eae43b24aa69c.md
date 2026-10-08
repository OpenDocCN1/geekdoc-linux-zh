# Hacking Exposed Web Applications

Once installed, UrlScan can be configured to reject HTTP requests based on the following criteria:

+   - The request method (or verb, such as GET, POST, HEAD, and so on)
- The file extension of the resource requested
- Suspicious URL encoding (see the section "IIS Directory Traversal" later in this chapter to understand why this may be important)
- Presence of non-ASCII characters in the URL
- Presence of specified character sequences in the URL
- Presence of specified headers in the request

The specific parameters for each of these criteria are set in the UrlScan.ini file, and more details about each criterion can be found in the UrlScan.doc file that comes with the IISLockdown utility.

> The UrlScan.ini file is only loaded when IIS is initialized and any changes to the configuration file require you to restart IIS before they take effect.

UrlScan.ini files are quite straightforward, and there are several templates that ship with the IISLockdown tool. Based on our cursory examination, the urlscan_static.ini template file is probably the most restrictive, as it is designed to limit a server's functionality to serving static HTML files via GET requests. Although we sometimes debate the wisdom of using an ISAPI filter to prevent attacks against IIS, UrlScan provides a powerful screening tool that allows administrators to granular control what requests reach their Web servers, and we highly recommend it if you run IIS.

See Appendix D for a complete discussion of UrlScan deployment and usage.

Monitoring and Logging Another countermeasure is to understand what to look for when an attack on an ISAPI DLL is underway or has successfully compromised a server. The of the most devastating outcomes of a buffer overflow with the ida/idq ISAPI extension mapping (see Table 3-1) were families of Internet-borne worms called Code Red and Nimda. Such worms spread like viruses across the Internet in 2001 and 2002 by infecting servers that were vulnerable to the buffer overflow and planting code that then went on to infect other servers. Web server logs on Code Red-infected servers contained entries similar to the following:

```
GET /default.ida?NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN
```