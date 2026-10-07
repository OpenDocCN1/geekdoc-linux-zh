# CHAPTER 20 News and Other Collaborative Communication

The leaf node does, however, have maintain a system for users to connect to the news server to read and post messages. This is often done by using UNIX, Microsoft Windows, or Apple Macintosh workstation software. Each client must connect to the leaf node to download articles from specific newsgroups, and it must upload postings made to the newsgroups. The leaf node must be able to forward new postings from customers to the newsfeed server.

# Local News Servers

An organization may not want to participate in the worldwide Usenet newsgroups but might want to use Usenet software to create its own news server to handle internal communications within the organization. Usually these communications need to remain private to the organization and don't need to be sent to all the Usenet hosts around the world. This is likely the most common use of a news server you might be asked to configure.

Two methods are used to implement a local news server. An organization may create a standalone news server that doesn't receive any newsfeeds from Usenet servers. The server contains only local newsgroups that are used for internal corporate communications. Alternatively, you can create on a Usenet server local newsgroups that aren't forwarded through any newsfeeds in the Usenet system. This allows organizations to create their own local newsgroups that their employees can participate in sharing their information with the rest of the world.

Thus, local newsgroups can be created on news servers that aren't connected to the Usenet network or that do not forward the local groups to their upstream newsfeeds. Any postings to the local newsgroups appear only on the local news server. The Usenet news servers. Usenet news servers allow clients to post articles to both the local and Usenet newsgroups. However, only articles posted to Usenet newsgroups are forwarded to the upstream news server. The local articles remain only on the local news server.

# Configuring a Local News Server

The InternetNews (INN) package is the most popular news server software used on UNIX servers. The Internet Software Consortium (ISC) currently maintains it, along with the INN Web site (http://www.isc.org/products/INN/). The Red Hat Linux distribution includes the INN package as a standard RPM file.

The following sections describe how the INN package works, how to install it, and how to configure it as a local news server. Because some users consider news servers to offer the greatest-server-challenges, the sections that follow are quite detailed. The information you'll learn here will help you avoid some of the common pitfalls while configuring your local news server.