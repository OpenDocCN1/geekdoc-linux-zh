
![](img/ec25e59d75726b7041242a56d3376832_241_0.png)

- Web server software
- Database software
- Server operating system

There are several techniques that we can use to gather this information directly from the browser. Most modern browsers include developer tools that can assist in the enumeration process. We will be focusing on Firefox since it is the default browser in Kali Linux. However, most browsers include similar developer tools.

### 9.2.1 Inspecting URLs

File extensions, which are sometimes a part of a URL, can reveal the programming language the application was written in. Some of these, like **php**, are straightforward, but other extensions are more cryptic and vary based on the frameworks in use. For example, a Java-based web application might use **jsp**, **do**, or **.html**.

However, file extensions on web pages are becoming less common since many languages and frameworks now support the concept of *routes*, which allow developers to map a URL to a section of code. Applications leveraging routes use logic to determine what content is returned to the user and make URI extensions largely irrelevant.

### 9.2.2 Inspecting Page Content

Although URL inspection can provide some clues about the target web application, most context clues can be found in the source of the web page. The Firefox *Debugger* tool (found in the *Web Developer* menu or by pressing **Ctrl** **Shift** **K**) displays the page’s resources and content, which varies by application. The Debugger tool may display JavaScript frameworks, hidden input fields, comments, client-side controls within HTML, JavaScript, and much more.

To demonstrate this, we can open the Debugger while browsing www.megacorp.one:

![](img/ec25e59d75726b7041242a56d3376832_242_0.png)

![](img/ec25e59d75726b7041242a56d3376832_242_1.png)

> *Figure 83: Using Developer Tools to Inspect JavaScript Sources*

We can see that the application running on www.megacorpone.com uses jQuery<sup>238</sup> version 1.11.0, a common JavaScript library. In this case, the developer minified<sup>239</sup> the code, making it more compact and conserving resources but making it somewhat difficult to read. Fortunately, we can “prettify” code within Firefox by clicking on the Pretty print source button with the double curly braces:

<sup>238</sup> (jQuery, 2019), https://jquery.com/

<sup>239</sup> (Wikipedia, 2019), https://en.wikipedia.org/wiki/Minification_(programming)

![](img/ec25e59d75726b7041242a56d3376832_243_0.png)

After clicking the icon, Firefox will display the code in a format that is easier to read and follow:

![](img/ec25e59d75726b7041242a56d3376832_243_1.png)

We can also use the Inspector tool to drill down into specific page content. Let’s use Inspector to examine the email input element from the "Contact" page by right-clicking the email address field on the page and selecting Inspect Element or using the shortcut Page Up.

![](img/ec25e59d75726b7041242a56d3376832_244_0.png)

![](img/ec25e59d75726b7041242a56d3376832_244_1.png)

This will open the Inspector tool and highlight the HTML for the element we right-clicked on.

![](img/ec25e59d75726b7041242a56d3376832_245_0.png)

*Figure 87: Using the Inspector Tool*

This tool is especially useful for quickly finding hidden form fields in the HTML source.

### 9.2.3 Viewing Response Headers

We can also search server responses for additional information. There are two types of tools we can use to accomplish this task. The first type of tool is a proxy, which intercepts requests and responses between a client and a webserver. We will explore proxies later in this module, but first we will explore the *Network* tool, launched from the *Firefox Web Developer* menu, to view HTTP requests and responses. This tool shows network activity that occurs after it launches, so we must refresh the page to see traffic.

![](img/ec25e59d75726b7041242a56d3376832_246_0.png)

*Figure 88: Using the Network Tool to View Requests*

We can click on a request to get more details about it, in this case the response headers:

![](img/ec25e59d75726b7041242a56d3376832_247_0.png)

*Figure 89. Viewing Response Headers in the Network Tool*

The "Server" header displayed above will often reveal at least the name of the web server software. In many default configurations, it also reveals the version number.

Headers that start with "X-" are non-standard HTTP headers.<sup>240</sup> The names or values often reveal additional information about the technology stack used by the application. Some examples of non-standard headers include X-Powered-By, x-amz-cf-id, and X-Aspnet-Version. Further research into these names could reveal additional information, such as the "x-amz-cf-id" header, which indicates the application uses Amazon CloudFront.

<sup>240</sup> (Mozilla, 2019). https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers

### 9.2.4 Inspecting Sitemaps

Web applications can include sitemap files to help search engine bots crawl and index their sites. These files also include directives of which URLs not to crawl. These are usually sensitive pages or administrative consoles—exactly the sort of pages we are interested in.

The two most common sitemap filenames are **robots.txt** and **sitemap.xml**.

For example, we can retrieve the **robots.txt** file from www.google.com with **curl**:

```text
kali@kali:~$ curl https://www.google.com/robots.txt
User-agent: *
Disallow: /search
Allow: /search/about
Allow: /search/static
Allow: /search/howsearchworks
Disallow: /sdch
Disallow: /groups
Disallow: /index.html?
Disallow: /?
Allow: /?hl=
...
```

*Listing 280 - https://www.google.com/robots.txt*

*Allow* and *Disallow* are directives for web crawlers indicating pages or directories that “polite” web crawlers may or may not access, respectively. Although the listed pages and directories in most cases may not be interesting and some may even be invalid, sitemap files should not be overlooked as they may contain clues about the website layout or other interesting information.

### 9.2.5 Locating Administration Consoles

Web servers often ship with remote administration web applications, or consoles, which are accessible via a particular URL and often listening on a specific TCP port.

Two common examples are the *manager*<sup>241</sup> application for *Tomcat* and *phpMyAdmin*<sup>242</sup> for MySQL hosted at */manager/html* and */phpmyadmin* respectively.

While these consoles can be restricted to local access or may be hosted on custom TCP ports, we often find them externally exposed by default configurations. Regardless, as penetration testers we should check the default console locations, identified in the application server software documentation. In the following section, we will also demonstrate tools that can be used to automate the search for these consoles and in a later section we will demonstrate exploitation techniques.

<sup>241</sup> (Apache Software Foundation, 2019). https://tomcat.apache.org/tomcat-7.0-doc/manager-howto.html

<sup>242</sup> (phpMyAdmin, 2019). https://www.phpmyadmin.net/

## 9.3 Web Application Assessment Tools

Once we have thoroughly explored a web application manually, we should consider using web application assessment tools to enumerate more information about the target.

There are a variety of tools that can aid in discovering and exploiting web application vulnerabilities, many of which come pre-installed in Kali. In this section, we will explore some of these tools including a few simple browser extensions and in a later section we will shift our focus to manual vulnerability enumeration and exploitation.

![](img/ec25e59d75726b7041242a56d3376832_249_0.png)

Automated tools can increase our productivity as penetration testers, but we must also understand manual exploitation techniques since tools will not always be available in every situation and manual techniques offer greater flexibility and customization. Remember, tools and automation make our job easier. They don't do the job for us.

### 9.3.2 DIRB

DIRB<sup>243</sup> is a web content scanner that uses a wordlist to find directories and pages by issuing requests to the server. DIRB can identify valid web pages on a web server even if the main index page is missing.

By default, DIRB will identify interesting directories on the server but it can also be customized to search for specific directories, use custom dictionaries, set a custom cookie or header on each request, and much more.

Let's run DIRB on www.megacorpone.com. We will supply several arguments: the URL to scan, **-r** to scan non-recursively, and **-z 10** to add a 10 millisecond delay to each request:

```text
kali@Kali:~$ dirb http://www.megacorpone.com -r -z 10
---
URL_BASE: http://www.megacorpone.com/
WORDLIST_FILES: /usr/share/dirb/wordlists/common.txt
OPTION: Not Recursive
SPEED_DELAY: 10 milliseconds
---------------------
GENERATED WORDS: 4612
----- Scanning URL: http://www.megacorpone.com/ ----
+ http://www.megacorpone.com/about (CODE:200|SIZE:12180)
+ http://www.megacorpone.com/admin (CODE:403|SIZE:292)
==> DIRECTORY: http://www.megacorpone.com/assets/
+ http://www.megacorpone.com/contact (CODE:200|SIZE:7721)
+ http://www.megacorpone.com/index (CODE:200|SIZE:12519)
+ http://www.megacorpone.com/index.html (CODE:200|SIZE:12519)
+ http://www.megacorpone.com/jobs (CODE:200|SIZE:11359)
==> DIRECTORY: http://www.megacorpone.com/old-site/
+ http://www.megacorpone.com/robots (CODE:200|SIZE:23)
+ http://www.megacorpone.com/robots.txt (CODE:200|SIZE:23)
+ http://www.megacorpone.com/server-status (CODE:403|SIZE:300)
---------------------
END_TIME: Wed Jun 5 11:03:05 2019
DOWNLOADED: 4612 - FOUND: 9
```

<sup>243</sup> (DIRB), https://github.com/fairsecurity/dirb
