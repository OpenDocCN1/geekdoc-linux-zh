the hosts defined inside. The format of the inventory files can be INItialization (INI) or YAML Ain't Markup Language (YAML).

The following code shows an example of one Inventory with INI format, which is the default used, defining two groups called webservers and observers, and having four servers in each group.

```
[webservers]
alpha.example.org
beta.example.org
192.168.1.100
192.168.1.110
[dbserver s]
db01.intranet.mydomain.net
db02.intranet.mydomain.net
10.25.1.56
10.25.1.57
```

As observed in the previous example, an inventory can contain a DNS-resolvable name or an IP. Groups can define systems with certain affinities, such as:

+   - **Geographically**: For example, hosts located in the same data center, city, or country.
+   - **Application**: Servers running similar applications, such as webs, databases, backup, and so on.
+   - **Operating system or distribution**: For example, to separate Linux and Windows systems, Ubuntu, and Red Hat Enterprise Linux systems.
+   - **Environment**: Such as development, test, production, and so on.

A host can be part of several groups, such as being part of development and webservers group. A host can have associated different parameters related to the connection or variables being used during the automation. Refer to the following example:

```
[linux]
rhel ansible_host=192.168.122.226 ansible_password=Start123
ubuntu ansible_host=192.168.122.43 ansible_password=Start123
```