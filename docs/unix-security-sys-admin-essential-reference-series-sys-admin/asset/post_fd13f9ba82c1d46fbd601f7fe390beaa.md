
## The Application-Level or Proxy Gateway

A lot of software in the networking community relies upon a store-and-forward approach (e.g., UUCP, electronic mail, and USENET news). The application collects the information, examines it, and then forwards it to the remote destination. Application-level gateways are service-specific forwarders or reflectors that operate at a user level, rather than a protocol level. When these services are running on a firewall, they become an essential element in the security of the entire private network.

The theory behind the application-level or proxy gateway is to restrict user interaction to a machine that does not itself provide the service the user is accessing. The proxy host provides additional authentication of the user, and keeps an audit trail to improve logging and allow the network administrator to see what the users of the various services are doing. The external user never sees the internal network, and therefore has no means of attacking it.

The advantage of this approach, in combination with any of the others, is that for each type of service you want to allow, you must add a gateway. For example, if you wanted to allow telnet services, then you would need to install a telnet proxy gateway; and similarly for ftp, and so on. In this situation, if the proxy service does not exist, then the application will not be permitted and access to the appropriate service will be denied.

### Figure 11.9 A sample screened subnet with machines added to support gopher, ftp, and World Wide Web services.

![](img/113bcc15fc2db8f0f40ac5d1e755f41c_127_0.png)

The disadvantage is that the development of these proxy gateway services is not trivial, and can be a serious stalling point. However, many of the software vendors who offer firewalls can provide application-level and proxy gateway services.

## The Hybrid Gateway

The hybrid gateway falls into a category other than those already mentioned. An example would be a serial connection to the Internet with a terminal server on the private network side. The more difficult the access to the internal network, the less likely that an attacker will spend the time necessary to break in. The hybrid gateway allows for the introduction of some rather esoteric ideas, such as tunneling one protocol over another, or using custom-designed software to monitor and examine the connections that are in place. An example is a site where the firewall consists of a hybrid gateway combined with a bastion host.

Hybrid gateways come in different shapes and sizes, and tend to be somewhat specific to the organization; thus, it isn't possible to describe exactly what such a gateway would look like. The obvious advantage to a hybrid gateway is that, if the security approach is nonstandard, then it becomes harder for an attacker to figure it out and more likely that the attacker will be discovered.

The trade-off here is security through obscurity versus the benefits of a well-documented and thoroughly understood security configuration. The more esoteric the scheme, the more difficult it becomes for the administrator to remember how it works and how the pieces fit together. The danger increases when the administrator is replaced by someone who was not involved in the process of designing the obscure gateway. It may ultimately be better to take a security approach that is easy to understand, document, and control.

Since hybrids are by definition eclectic, it isn't possible to generalize about their vulnerability to attack or about the risk involved in running this type of firewall. One obvious requirement is that the organization have the internal resources to design, build, and maintain the system without having to rely upon outside resources. It seems likely that with the continued expansion of the Internet, methods for developing hybrid gateways will become better known and will allow more security options for the administrator.

## Firewall Tools

Vast collections of tools and numerous vendors offer software and security products and services. Even though firewalls are relatively new, they are fast becoming a major part of the network security business. I recommend that you examine publicly available code very carefully before trusting it to protect your network. This caution is not meant to imply that the code itself may be questionable, but to ensure that what you think you are getting is actually what you want. The sidebar, “Publicly Available Tools,” lists a number of popular tools and explains how to get them.

## Conclusion

If you are considering whether or not to use a firewall, be sure to answer the following questions.

- From whom are we protecting ourselves?
- What are we trying to protect?
- How valuable is the information we are trying to protect?
- How important is Internet access to our users?
- How important is access to our network from the Internet?

Once you have addressed these questions, the issue becomes a matter of selecting the firewall method that best meets the needs of your organization, its users, and clients.

## Reference

Hare, Chris and Karanjit Siyan. Internet Firewalls and Network Security, 2nd ed. Indianapolis: New Riders Publishing. 1996.
