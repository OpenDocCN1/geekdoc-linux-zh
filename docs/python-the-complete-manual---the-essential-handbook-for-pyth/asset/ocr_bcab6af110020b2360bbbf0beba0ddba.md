# Python for system administrators

# Work with Python

So, you want to use some Yahoo! APIs...
We need some information from you to use Yahoo Web Services, we need some information about the application you're building. We use this information to get a better understanding of how Yahoo Services are being used and to protect the security and privacy of Yahoo users. All questions are required.

| SUBMIT THIS FORM | GET YOUR ADDRESS | WRITE YOUR CODES |

About your application

| Application Name: | LudySearch |
| --- | --- |
| Kind of Application: | Client/Desktop |
| Description: | An App to demonstrate the JSON parsing using Python 260 characters or less |

Favicon URL: http://www.yahoo.com/this/App/Favicon.gif
Optional: specify a URL to a 16x16 JPG, PNG or GIF image.

# Security & Privacy

Yahoo APIs use the OAuth protocol for secure validation of API usage and end-user authentication, if needed.
Access Scopes: This app will only access public APIs, Web Services, or RSS feeds. This app requires access to private data.

# Contact information

Just in case comes up and we need to get help from you:
Application Owner: Kunal Desai
Contact Email: kunals2001@yahoo.com
Terms of Use: I have read and agree to the Yahoo Developer Network Terms of Use.

| Get API KEY | Cancel |

Generating the Yahoo App ID

```
starting with '>>>' indicate input
>>> executefile('LudySearch.py')
>>> results = search('Linux User and Developer')
>>> results['totalResultsAvailable']
123000000
>>> results['totalResultsReturned']
20
>>> items = results['Result']
>>> For Result in items:
    print Result['Title'],Result['Url']
```

encyclopedia http://en.wikipedia.org/wiki/Linux_User_and_Developer
Linux User &amp; Developer | Linux User http://www.linuxuser.co.uk/linux-user-developer/

# Gathering system information

An important job for a system administrator is gathering system information. Here we will use the SIGAR (System Information Gathering And Reporter) API to demonstrate how we can gather information using Python. SIGAR can provide lots of information, including:

+   1. System memory, swap, CPU, load average, uptime, logins.

Linux User http://www.linuxuser.co.uk/
Linux User and Developer - Wikipedia, the free

![](bbox=[0.663, 0.915, 0.703, 0.995])