Tip
You should maintain separate names for your NIS and DNS domains for two reasons. First, it is easier for you to differentiate what you're talking about when discussing problems with anyone else. Second, having separate names makes it more difficult for potential intruders to understand the internal workings of your machines from the outside.

Both the clients and servers bind themselves to a domain; hence, a client can only belong to one NIS domain at a given time. Once bound, clients send a broadcast to find the NIS server for the given domain.

# The Different Servers

So far, you might have noticed that I've referenced the NIS server explicitly as the *master* server. The two kinds of NIS servers are master servers and slave servers.

*Master* NIS servers are the actual truth holders. They contain the text files used to generate the DBM files, and any changes to the database must be made to these files.

*Slave* NIS servers are designed to supplement master NIS servers by taking some of the load off. When a file is updated on the server, a server push is initiated and the slave NIS server gets an updated copy of the DBM files.

Caution
Like any network service, NIS might have bugs that can allow unauthorized access to your system. It is prudent to keep track of security reports and obtain patches when they become available. The two best places to start are the Computer Emergency Response Team Web site at www.cert.org and the comp.os.linux.announce newsgroup. Both provide a moderated source of information that you can use to maintain your system.

# Installing the Software

If you didn't install the NIS software during the initial setup process, you need to install it now. Start by mounting the Red Hat CD-ROM. The following assumes that the CD-ROM is mounted on the /mnt/cdrom directory.