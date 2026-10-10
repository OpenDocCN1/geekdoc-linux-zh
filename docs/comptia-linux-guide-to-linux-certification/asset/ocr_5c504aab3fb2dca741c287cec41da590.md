that others see and respond to. Newsgroup forums are grouped according to topic. Posting to a newsgroup is often a very quick way to find the solution to a problem because people who read the posting are likely to have had the same problem and found the solution. In addition, newsgroup forums can be moderated, in that a person or group responsible for the forum edits messages before they are posted to ensure they fit the forum's theme. This ensures proper newsgroup etiquette, which dictates that before posting a question you search previous postings to ensure that the question has not already been asked and answered and that only messages relevant to the newsgroup topic are posted.

Many OSS developers use newsgroups to exchange information and coordinate software creation. As with e-mails, a special program called a newsreader is necessary to access news- groups and read postings hosted on news servers. Common Linux newsreaders include Gnnews, PAN, Gnus, Thunderbird, and pine. The most popular open source news server soft- ware available for Linux is called InterNettworkNews (INN); it is included with most com- mon Linux distributions and is maintained by an open source organization called the Inter- net Systems Consortium, which continually develops and improves several open source Internet technologies.

> For more information on how to subscribe to newsgroups, visit *groups.google.com*.

![](bbox=[0.08, 0.46, 0.28, 0.52])

# **DNS Services**

Each computer on a network needs a unique way to identify itself and to refer to other computers. This is accomplished by assigning each computer a number called an **Internet Protocol (IP) address**. An IP address is a long string of numbers that would be very hard for the typical person to remember. Thus, IP addresses are often associated with more user-friendly names. In particular, servers are identified by names like *www.linux.org*, which are known as **fully qualified domain names (FQDNs)**. When you use a Web browser such as Internet Explorer or Netscape Navigator to request information from a Web server, you typically type the Web server’s FQDN (e.g., *www.linux.org*) into your browser’s address bar. However, FQDNs exist only for the convenience of the human beings who use computer networks. The computers themselves rely on IP addresses. Thus, before your browser can retrieve the requested information from the Web server, it needs to know the IP address associated with the FQDN you typed into the address bar. Your browser gets this information by contacting a server hosting the Domain Name System (DNS). The DNS server maintains a list of the proper FQDN to IP mappings and quickly returns the requested IP address to your browser. Your browser can then use this IP address to connect to the target Web site.

For companies wanting to create a DNS server, Linux is an inexpensive solution, as many distributions of Linux ship with a Domain Name System known as BIND (Berkeley Internet Name Domain).

> Each computer participating on the Internet must have an IP address.

![](bbox=[0.08, 0.92, 0.28, 0.98])