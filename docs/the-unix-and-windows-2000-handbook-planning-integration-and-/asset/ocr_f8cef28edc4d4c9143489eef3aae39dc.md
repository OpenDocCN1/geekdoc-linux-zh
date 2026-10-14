ability to dynamically assign addresses. It gets interesting when the ability to dynamically register a machine name is added to network address mapping. Traditional DNS servers rely on static address tables, while WINS is purely dynamic, meaning the client machine provides the registration information to the WINS server. Recently, Dynamic DNS has emerged with the introduction of Windows 2000. With this new version of DNS, it will be possible to have a completely dynamic name registration system.

At the conclusion of this chapter, you should have a good understanding of DNS, WINS, and DHCP. With the tips and tools contained here, you will be able to manage most of the day-to-day name resolution services of your network.

# Name Resolution Using DNS

During the infancy of the Internet, keeping track of all the attached systems was easy. A single file contained the list of all IP addresses and hostnames associated with each address. As a system administrator, if you were lucky enough to have one of the few connected systems, all you needed to do was to FTP the list once every two or three weeks to keep up-to-date with the latest new systems that came on-line. Life was simple when the growth of the Internet was slow.

However, as the Internet grew, new systems were added at an ever-increasing rate. The master list of Internet IP hostnames became more and more difficult to maintain, and system administrators needed to update their copy of the file daily to keep up. Due to the difficulty in managing this simple file, DNS was born.

DNS is a conglomeration of all the possible domain namespaces that are currently recognized. In the beginning, the domain namespaces consisted of simple domains such as .com, .gov, .edu and .org. However, with the huge growth of the Internet, many new namespaces were added, including .net, .mil, and a namespace for each country on the planet. While not a simple process to manage, the fine folks at the Network Information Center, commonly know as the Internic, have taken responsibility for assigning and maintaining the data and conventions that make up the top level, or the root of DNS. For more information about the Internic, you can visit them at www.internic.net.

# UNIX NAME RESOLUTION

Translating IP addresses into hostnames and vice versa in UNIX is accomplished by using one or more of the following techniques: