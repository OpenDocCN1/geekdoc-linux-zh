this unsanitized input is displayed on a web page, this creates a Cross-Site *Scripting* (XSS)²⁵⁷ vulnerability.

Once thought to be a relatively low-risk vulnerability, XSS today is both high-risk and prevalent, allowing attackers to inject client side scripts, such as JavaScript, into web pages viewed by other users.

There are three Cross-Site Scripting variants: stored,²⁵⁸ *reflected*,²⁵⁹ and DOM-based.²⁶⁰

*Stored XSS attacks*, also known as *Persistent XSS*, occurs when the exploit payload is stored in a database or otherwise cached by a server. The web application then retrieves this payload and displays it to anyone that views a vulnerable page. A single Stored XSS vulnerability can therefore attack all users of the site. Stored XSS vulnerabilities often exist in forum software, especially in comment sections, or in product reviews.

*Reflected XSS attacks* usually include the payload in a crafted request or link. The web application takes this value and places it into the page content. This variant only attacks the person submitting the request or viewing the link. Reflected XSS vulnerabilities can often occur in search fields and results, as well as anywhere user input is included in error messages.

*DOM-based XSS attacks* are similar to the other two types, but take place solely within the page’s Document Object Model (DOM).²⁶¹ We won’t get into many details at this point, but a browser parses a page’s HTML content and generates an internal DOM representation. JavaScript can programmatically interact with this DOM.

This variant occurs when a page’s DOM is modified with user-controlled values. DOM-based XSS can be stored or reflected. The key difference is that DOM-based XSS attacks occur when a browser parses the page’s content and inserted JavaScript is executed.

Regardless of how the XSS payload is delivered and executed, the injected scripts run under the context of the user viewing the affected page. That is to say, the user’s browser, not the web application, executes the XSS payload. Still, these attacks can have a significant impact resulting in session hijacking, forced redirection to malicious pages, execution of local applications as that user, and more. In the following sections, we will explore some of these attacks.

# 9.4.2.1 Identifying XSS Vulnerabilities

We can find potential entry points for XSS by examining a web application and identifying input fields (such as search fields) that accept unsanitized input which is displayed as output in subsequent pages.

Once we identify an entry point, we can input special characters, and observe the output to see if any of the special characters return unfiltered.

+   ²⁵⁷ (Wikipedia, 2019), https://en.wikipedia.org/wiki/Cross-site_scripting
+   ²⁵⁸ (Wikipedia, 2019), https://en.wikipedia.org/wiki/Cross-site_scripting#Persistent_(or_stored)
+   ²⁵⁹ (Wikipedia, 2019), https://en.wikipedia.org/wiki/Cross-site_scripting#Non-persistent_(reflected)
+   ²⁶⁰ (Wikipedia, 2019), https://en.wikipedia.org/wiki/Cross-site_scripting#Server-side_versus_DOM-based_vulnerabilities
+   ²⁶¹ (Wikipedia, 2019), https://en.wikipedia.org/wiki/Document_Object_Model