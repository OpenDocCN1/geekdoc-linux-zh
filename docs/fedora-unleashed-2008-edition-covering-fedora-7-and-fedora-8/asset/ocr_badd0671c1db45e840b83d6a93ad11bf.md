# # CHAPTER 22  
# Setting Up a Proxy Server

+   - 	What Is a Proxy Server?
+   	- Installing Squid
+   	- Configuring Clients
+   	- Access Control Lists
+   	- Specifying Client IP Addresses
+   	- Sample Configurations
+   	- Reference

There are two things in this world that you can never have enough of: time and bandwidth. Fedora comes with a proxy server—Squid—that enables you to cache web traffic on your server so that websites load faster and users consume less bandwidth.

# ## What Is a Proxy Server?

A proxy server lies between client machines—the desktops in your company—and the Internet. As clients request websites, they do not connect directly to the web and send the HTTP request. Instead, they connect to the local proxy server. The proxy then forwards their requests on to the web, retrieves the result, and hands it back to the client. At its simplest, a proxy server really is just an extra layer between client and server, so why bother?

The three main reasons for deploying a proxy server are

+   - **Content control**—You want to stop people whiling away their work hours reading the news or downloading MP3s.
+   	- **Speed**—You want to cache common sites to make the most of your bandwidth.
+   	- **Security**—You want to monitor what people are doing.

Squid is capable of achieving all of these goals and more.