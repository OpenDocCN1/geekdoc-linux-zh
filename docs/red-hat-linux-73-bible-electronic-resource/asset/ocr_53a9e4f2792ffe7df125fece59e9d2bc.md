# Chapter 25

# Making Servers Public with DNS

# In This Chapter

+   • Determining goals for your server
+   • Connecting a public server
+   • Configuring a public server
+   • Setting up a DNS server

You learned in previous chapters how to build your own Web, mail, and FTP servers in Linux. Now perhaps you want to expose those servers to the outside world. Your options range from handing off your server to a hosting company and saying, “Take care of it,” to completely managing the servers yourself out of your own home or office.

The following are some cases where you may want to consider some level of self-hosting:

+   • You’re willing to provide the level of service and support that your organization needs in its servers.
+   • You just want an inexpensive way to publish some documents on the Web or maintain a public mail server for a few people and 24-7 support isn’t critical.
+   • You just think self-hosting is cool and you want to try it.

The first goal of this chapter is to help you decide how much support of your servers you want to maintain or give to someone else. The second is to suggest how to set up your own public servers, including possibly configuring your own Domain Name System server.

The descriptions of setting up your local area network (Chapter 15) and connecting it to the Internet (Chapter 16) focus on how to share information locally and enable your local users to share an outgoing Internet connection, respectively. Building on that information, this chapter describes how to set up your own DNS server, as well as many other issues that relate to securing and maintaining public servers.