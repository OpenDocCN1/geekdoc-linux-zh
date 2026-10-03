# APPLY YOUR KNOWLEDGE

12. B. Each line of the /etc/nsswitch.nis file identifies a particular type of network information, such as host, password, and group; followed by one or more sources, such as NIS+ tables, NIS maps, the DNS hosts table, or the local /etc.

13. B. The following entry in the nsswitch.nis template: hosts: nis [NOTFOUND=return] files states that only the NIS hosts table in the NIS map is searched.

14. A., C. The following template files are available: nsswitch.files, nsswitch.nisplus, nsswitch.nis, nsswitch.dns, and nsswitch.ldap

15. B. The arrangement of a NIS+ namespace can vary from site to site; all sites use the same structural components: directories, tables, and groups. These components are called objects, and they can be arranged into a hierarchy that resembles a UNIX file system.

16. A. The four authorization classes of NIS+ are Owner, Group, World, and Nobody.

17. D. Access rights are similar to file permissions. There are four types of access rights: read, modify, create, and destroy.

18. C. There are three security levels: 0, 1, and 2.

19. D. Security level 2 is the default. It is the highest level of security currently provided by NIS+.

20. A. DNS is the name service provided by the Internet for Transmission Control Protocol/Internet Protocol (TCP/IP) networks.

21. B. Each server implements DNS by running a daemon called in.named.

22. B. The process of finding a computer's IP address by using its host name as an index is referred to as name-to-address resolution, or mapping. The primary task of DNS is to provide name-to-address resolution.

23. A. Authentication is used to identify NIS+ principals. A NIS+ principal can be a client user or a client workstation. Every time a principal (user or system) tries to access a NIS+ object, the user's identity and secure RPC password are confirmed and validated. Authorization is used to specify access rights.

24. A. The /etc/nsswitch.conf file determines how a particular type of information is obtained and in which order the naming services should be queried.

25. C. There are five name services that Solaris 8 supports: /etc files, NIS, NIS+, DNS, and LDAP.

26. A. DNS is the name service used by the Internet.

27. D. To build new maps on the master server, type: /usr/sbin/ypinit -m.