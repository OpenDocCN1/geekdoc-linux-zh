+   * hint—A hint zone is only really used in connection with the initial list of potential root servers, found in `/etc/namedb/named.root`. This initial list is not actually the authoritative list of root servers; it's a list of “hints” for BIND, specifying servers that will have the current true list of root servers. The contents of the true list has a habit of changing as network conditions vary.

# ## Restricting DNS Access

BIND has the capability to restrict access based on Access Control Lists (ACLs). ACLs are not a requirement, but they can make configuring your server much simpler, allowing you to use shorthand names for lists of addresses that you tend to reuse. An ACL is specified in an **acl** statement, which defines a name for the list and contains the criteria for which hosts are included in the list. These criteria can take a number of forms, and they can be recursive; in other words, an ACL can contain other ACLs. The following ACLs are pre-defined for you:

+   * **any**—Allows all hosts
+   * **none**—Denies all hosts
+   * **localhost**—Allows the IP addresses of all interfaces on the system
+   * **localnets**—Allows any host on a network for which the system has an interface

Other types of list elements that are allowed can be IP addresses (for instance, 111.112.113.114), networks in CIDR format (for instance, 111.112.113/24), a “negated” version of either of these (111.112.113.114, which means “any host but 111.112.113.114”), or a **key** statement (used in secure DNS transactions, which are beyond the scope of this chapter). When you’re compiling a list of ACL elements, it’s best to put the more specific elements before the broader ones because the list is evaluated in the order in which it’s specified. If a host matches any element, it will be allowed, regardless of whether a later “negation” element would have matched it. Put all such exceptions toward the beginning of the list.

Because `named.conf` is read sequentially, an ACL must be specified in the file before it can be referred to later in other statements. For best results, put all **acl** statements toward the top of your `named.conf` file, above the **options** block. A sample ACL would be the following:

```
acl "my_list" {
 localhost;
 localnets;
 another_list;
 !132.112.14.124;
 132.112.14/24;
};
```