In today’s world, where practically everything revolves around the Internet, making your applications network accessible is almost a necessity. Fortunately, there’s plenty of help available in the Ubuntu server distribution. The Ubuntu server distribution is created specifically for running server applications, as opposed to desktop applications. It provides two popular web server packages for you to install, the Linux-Apache-MySQL-PHP (LAMP) platform, as well as the Tomcat Java application server. Mostly due to its simplicity and robustness, the LAMP platform has quickly become one of the hottest web application platforms on the Internet. The Tomcat Java application server provides an environment for creating JavaServer Pages (JSP) applications as well as Java servlets applications, both extremely popular in the Java programming world. This chapter describes the Ubuntu server web platform as installed from the Ubuntu server distribution and walks you through setting up and using both the LAMP and Tomcat servers.

# Ubuntu Web Servers

With literally millions of web pages on the Internet, and more springing up every day, it’s getting harder to attract and impress online visitors. Having outdated information on your web page will not only frustrate your visitors, but it might even damage your company or organization. To avoid this problem, web pages must be dynamic.

Dynamic web pages allow you to change your content in real time, without having to touch any of the code used to create the page. With dynamic web pages you can keep the content fresh so that what visitors see there now may be updated or replaced the next time they visit, whether that’s a week from now, tomorrow, or the next hour. The core layout of the web page can remain the same (such as corporate logos, links, and headings), but the data presented on the page constantly change.

The key to doing this without keeping a full-time staff of web site designers busy is to use *web scripting languages*. Web scripting languages allow you to incorporate programming code within your web pages that can access external data and display them just as if the data had been coded into your web page.

The following section walks through how web scripting languages work, then it discusses the three types of web scripting languages installed on the Ubuntu server.

# Web Scripting Languages

The client browser displays only what the web server sends it. For a dynamic web page to change what it sends to visitors in real time, the HTML coding must be able to automatically change. To accomplish this, developers embed programming code using a scripting language within the HTML code. As the embedded program runs, it automatically changes the content (or layout) of the web page without any intervention from the web designer. Figure 21-1 demonstrates this process.

The embedded program code generates standard HTML code that the client browser interprets. Because programming code is embedded in the dynamic web page, something somewhere must run the code to produce the HTML for the new content.

The embedded programming code can run in two places:

+   - **Client side:** on the client's workstation after it downloads the web page
+   - **Server side:** on the web server before the web page is sent