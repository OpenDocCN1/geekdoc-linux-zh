One of the most common computer networking buzzwords these days is firewall. Small companies and even individuals post to various newsgroups asking for advice on purchasing a firewall or configuring a computer as one. Employees gripe that their companies’ firewalls interfere with their use of the Internet. Companies seek out network administrators with experience configuring custom firewalls.

Ideally, a firewall goes unnoticed by legitimate users of a system while simultaneously blocking access by would-be crackers. Unfortunately, this ideal is difficult to attain. Like many aspects of computer security, it’s easy to configure a firewall to be transparent to users but not very secure, or secure but a major nuisance to users. Implementing security and ease of use is hard. The goal of this chapter is not to present everything you need to know about firewalls; entire books have been written about firewalls, and I can only present some basics in this chapter. After reading this chapter, though, you should know enough to determine what type of firewall you want, the general steps involved in configuring one, and where to go to find the details.

If you haven’t already done so, you may want to read Chapters 2, “Understanding TCP/IP,” and 3, “Networking Services.” Firewall technologies often interact with different layers of the TCP/IP stack, ports, and so on, so it’s important that you be familiar with these concepts when you learn about and configure a firewall.

# Understanding Firewalls

The first step on the road to firewall installation is to understand what a firewall is, what it can do, and when the use of a firewall may be useful to you. This section covers these issues.

# What Is a Firewall?

Most generally, a firewall is a network device that controls the flow of data between two networks. This may sound similar to a router (p. 87), but an ordinary router is a fairly passive device; it merely passes packets uncritically from one network to another. A firewall, by contrast, examines the packets to one extent or another and makes a decision about what to do with them.

In this chapter, I discuss two different types of firewalls: packet filters and proxy servers. These terms aren’t used universally; for instance, some people refer to them as chokes and gates, respectively. Others may consider packet filters in a class by themselves, separate from firewalls. If you do further reading on firewalls, you should be aware of these differences in terminology.