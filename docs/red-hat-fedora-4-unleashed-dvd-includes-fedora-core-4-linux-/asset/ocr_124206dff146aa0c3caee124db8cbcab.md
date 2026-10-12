# CHAPTER 28

# News Servers and Mailing Lists

# IN THIS CHAPTER

+   - Types of News Servers
+   - The INN Package and Configuration Files
+   - Installing the INN Package
+   - Configuring innd
+   - Reference

There are many advantages to hosting your own local news server. If you have a number of clients on your network who need frequent access to a central site of information or you need to provide employees with a central collaboration site or forum, news servers can provide a simple way of getting information to them in a public and easy-to-use way.

News servers are notoriously difficult to configure and deploy, but follow the information in this chapter and you will be able to avoid many of the problems that are frequently encountered.

# Types of News Servers

The InterNetNews (INN) package is the most popular news server software on Unix servers. The Internet Software Consortium (ISC) currently maintains it, along with the INN website (http://www.isc.org/products/INN/). The Fedora Core Linux distribution includes the INN package as a standard RPM file.

The following sections describe how the INN package works, how to install it, and how to configure it as a local news server. Because some users consider news servers to offer the greatest server-configuration challenges, these sections are quite detailed. The information you learn here will help you avoid some of the common pitfalls while configuring your local news server.

Unless you are an Internet service provider (ISP) or are planning to provide news services to a large group of people, you will likely not be setting up or administering a news server for your own use.