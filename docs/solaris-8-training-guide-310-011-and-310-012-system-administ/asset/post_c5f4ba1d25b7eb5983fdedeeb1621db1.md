
## APPLY YOUR KNOWLEDGE

You will be asked to identify the NIS server from which the client can obtain name service information. Type the NIS master server name, followed by a carriage return.

When asked for the next host to add, press Ctrl+D.

5. Start the NIS daemons by executing the following script:
`/usr/lib/netsvc/yp/ypstart`

6. Verify that the NIS client is bound to the NIS master by typing:
`ypwhich`

The master server name should be displayed.

7. Test the NIS client by logging out and logging back in using a login name that is no longer in the local /etc/passwd file and is managed by NIS.

## Review Questions

1. Which of the following services stores information that users, systems, and applications must have to communicate across the network, in a central location?
- A. NIS service
- B. NFS service
- C. Automount
- D. AutoFS

2. Which of the following is not a Solaris name service?
- A. DES
- B. /etc
- C. NIS+
- D. DNS

3. Which of the following is the traditional UNIX way of maintaining information about hosts, users, passwords, groups, and automount maps?
- A. DNS
- B. NIS
- C. NIS+
- D. /etc

4. The NIS administration databases are called:
- A. Files
- B. Tables
- C. Maps
- D. Objects

5. The set of maps shared by the servers and clients is called:
- A. A table
- B. An object
- C. The NIS domain
- D. None of the above

6. When you add a new system to a network running NIS, you have to update the input file in the master server and run:
- A. makedbm
- B. make
- C. yppush
- D. ypinit

7. Which of the following commands is used to display the values in a NIS map?
- A. ypcat
- B. ypwhich
- C. ypserv
- D. ypbind

8. Which of the following commands can be used to determine which server is the master of a particular map?
- A. ypbind
- B. ypcat
- C. ypserv
- D. ypwhich

9. Which of the following propagates a new version of a NIS map from the NIS master server to NIS slave servers?
- A. ypinit
- B. yppush
- C. make
- D. yppoll

10. Which of the following sets up master and slave servers and clients to use NIS?
- A. makedbm
- B. make
- C. ypinit
- D. yppush

11. Which of the following is the configuration file for the name service switch?
- A. nsswitch.conf
- B. resolve.conf
- C. /etc/netconfig
- D. nsswitch.nis

12. Each line of which of the following files identifies a particular type of network information, such as host, password, and group; followed by one or more sources, such as NIS+ tables, NIS maps, the DNS hosts table, or local /etc?
- A. resolve.conf
- B. nsswitch.conf
- C. /etc/netconfig
- D. nsswitch.nis

13. In the name service switch file, what does the following entry mean?
hosts: nis [NOTFOUND=return] files
- A. Search the NIS map and then the local /etc/hosts file.
- B. Search only the NIS hosts table in the NIS map.
- C. Search only the local files, not the NIS files.
- D. Do not search the NIS hosts table or the local /etc/hosts file.

14. Which name service switch template files are found in Solaris 8?
- A. nsswitch.files
- B. nsswitch.nis+
- C. nsswitch.nisplus
- D. nsswitch.fns

15. The components of a NIS+ namespace are called:
- A. Tables
- B. Objects
- C. Maps
- D. Directories

16. Which of the following is not one of the four authorization classes of NIS+?
- A. All
- B. Owner
- C. Group
- D. Nobody

17. What are the four types of NIS+ access rights?
- A. read, write, create, modify
- B. read, write, execute, no access
- C. read, write, delete, modify
- D. read, modify, create, destroy

18. How many security levels are there in NIS+?
- A. 2
- B. 1
- C. 3
- D. 4

19. Which security level is the default in NIS+?
- A. 3
- B. 0
- C. 1
- D. 2

20. Which of the following is the name service provided by the Internet for TCP/IP networks?
- A. DNS
- B. NIS
- C. NIS+
- D. None of the above

21. Each server implements DNS by running a daemon called
- A. named
- B. in.named
- C. nfsd
- D. dnsd

22. The primary task of DNS is to provide
- A. security service
- B. name-to-address resolution
- C. name service
- D. namespace services

23. Which of the following describes the difference between NIS authentication and authorization?
- A. Authentication is checking if the information requester is a valid user on the network, and authorization determines whether the particular user is allowed to have or modify the information.
- B. Authorization is checking if the information requester is a valid user on the network, and authentication determines whether the particular user is allowed to have or modify the information.

24. Entries in which of the following files determine how a particular type of information is obtained (that is, which naming services (NIS, NIS+, DNS, etc.) can be used to obtain which types of information (host, password, group) and in which order the naming services should be queried)?
- A. /etc/nsswitch.conf
- B. /etc/resolve.conf
- C. /etc/nsswitch.nis
- D. /etc/nsswitch.nisplus

25. How many name services does Solaris 8 support?
- A. 3
- B. 4
- C. 5
- D. 6

26. Which of the following is the name service used by the Internet?
- A. DNS
- B. NIS
- C. NIS+
- D. DES

27. Which of the following commands is used to set up a NIS master server?
- A. ypserver -m
- B. nisinits -m
- C. nisserver -m
- D. ypinit -m

## Answers to Review Questions

1. A. NIS stores information about workstation names and addresses, users, the network itself, and network services.
2. A. DES is not a Solaris name service.
3. D. /etc files are the traditional UNIX way of maintaining information about hosts, users, passwords, groups, and automount maps.
4. C. The NIS administration databases are called maps.
5. C. The set of maps shared by the servers and clients is called the NIS domain.
6. B. To update the input file in the master server with a new system name, you’ll execute the /usr/ccs/bin/make command.
7. A. Just as you use the cat command to display the contents of a text file, you can use the ypcat command to display the values in a map.
8. D. You can use the ypwhich command to determine which server is the master of a particular map.
9. B. The command yppush propagates a new version of a NIS map from the NIS master server to NIS slave servers.
10. C. The ypinit command builds and installs a NIS database and initializes the NIS client’s (and server’s) ypservers list.
11. A. In setting up the NIS service, set up the name service switch, which involves editing the /etc/nsswitch.conf file.
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
