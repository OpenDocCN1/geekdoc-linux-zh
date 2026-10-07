# CHAPTER 20 News and Other Collaborative Communication

```
newsgroups: "*"
access: RPA
}
auth "localnet" {
  hosts: "192.168.*"
  default: "<user>
  default-domain: "isp.net"
}
```

```
access "localnet" {
  users: "**@isp.net"
  newsgroups: "*"
  access: "RP"
}
```

The sample readers.conf file defines here two separate groups of users. The first group, called localhost, allows the local host, address 127.0.0.1, address 192.168.1.100 (the local host's network address), and any connection using the standard input to connect to the news server. The unmodified readers.conf file provided by Red Hat allows only access from the local host.

The second group defines any client located on the 192.168. network; it allows both reading and posting of all newsgroups to any client on the network. You can adjust the addresses as necessary for your network.

# The active and newsgroups Files

The active and newsgroups files, although not specifically identified as configuration files, are crucial to the operation of the news server. These files control what newsgroups your news server can handle. Each newsgroup handled by the news server must have an entry in both the active and newsgroups files. Both of these are located in the /var/lib/news directory when they are installed using the Red Hat RPM package.

The syntax of the active file is as follows:

```
newsgroup      first      last      post
```

Each newsgroup handled by the news server is defined on a separate line in the active file. The Red Hat Linux INN configuration supplies a skeleton active file that defines several newsgroups:

```
control 0000000000 0000000001 n
control.cancel 0000000000 0000000001 n
control.checkgroups 0000000000 0000000001 n
control.newgroup 0000000000 0000000001 n
control.rmgroup 0000000000 0000000001 n
junk 0000000000 0000000001 n
```