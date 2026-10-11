# **Chapter 15: Web Servers in Linux**

# **Introduction**

A Web server is a computer that runs software that serves up Web pages. When you visit a Web site such as that for this book's publisher, www.charlesriver.com/, your browser connects to that machine, probably after connecting to your Internet service provider and a veritable host of intermediate sites or routers, and requests an HTML document from that machine. That machine then serves up that HTML document, and thus we have a Web server. That explains what a Web server is, but not why you might want one. In earlier chapters we discussed briefly how to develop our own Web pages, using some of the tools that come with Red Hat Linux 9.0. You can then use a commercial or free Web hosting service. But what if you want to host those Web pages from your home machine? Or what if you are administering a small network in an office and want to provide a Web site for the office, or just an internal Web site for people in that office to use? In any of these scenarios you might want your own Web server. Fortunately for you, Linux provides such Web servers.

Red Hat ships with a very popular Web server, the Apache server, which we will examine in detail in this chapter. There are also several free or low-cost Web servers you can download from the Internet. We will briefly discuss some of these later in this chapter. At the end of this chapter you should have a basic understanding of what Web servers are, how they work, and how to set up the Apache Web server.

# How Do Web Servers Work?

It is possible that you could set up and run the Apache Web server and not really understand how it is working. Such a course of action is bound to be fraught with problems. Anytime you are operating technology and have no idea how or why it works, you are asking for problems. For this reason we will take a few moments to discuss how Web servers work and communicate.

To begin with, recall that every type of communication that a computer does is handled by some sort of protocol. You have already learned that e-mail is sent using SMTP (Simple Mail Transfer Protocol) on port 25 and received using POP3 (Post Office Protocol Version 3) on port 110. You also learned that files are uploaded or downloaded on the Internet using FTP (File Transfer Protocol), and it works on port 21. Web communication is no different. It uses HTTP (Hypertext Transfer Protocol) and works on port 80.

HTTP works by requests and responses. A Web browser sends a specific request to an address. That address can be either an IP address such as 10.10.10.01 or a URL such as www.chuckeasttom.com. The Web server that is at that address then sends back a specific response. In essence a Web server is any computer that has some program on it that can listen to port 80 and respond to the HTTP requests it receives.

**Note** Just for your information, IP stands for Internet Protocol, and URL stands for Uniform Resource Locator. It is basically just a technical way of saying Web address.

How does a Web server respond when it gets this request? It begins by sending back a numeric code to the Web browser that sent the request. That code tells the browser what is happening on the server side. Have you ever seen a Web page response like "HTTP 404 - File Not Found," as shown in Figure 15.1a? The number 404 is the error code that all Web servers send to browsers if they cannot find the Web page that the browser requested.