```
DROP    tcp -- 192.168.2.76    anywhere    tcp dpt:smtp
```

```
Chain FORWARD (policy ACCEPT)
target  prot opt source    destination
```

```
Chain OUTPUT (policy ACCEPT)
target  prot opt source    destination
```

The rule may subsequently be removed as follows:

```
# iptables -D INPUT -s 192.168.2.76 -p tcp --destination-port 25 -j DROP
```

Given the complexity of iptables it is unsurprising that several user-friendly configuration tools have been created to ease the rule creation process. One such tool is the firewall-cmd command-line tool which will be covered in the chapter “RHEL 9 Firewall Configuration with firewalld”.

# 13.4 Well-Known Ports and Services

Before moving on to cover more complex firewall rules, it is first worth taking time to outline some of the key services that can be provided by an RHEL 9 system, together with the corresponding port numbers:

| Port | Assignment | Description |
|------|------------|-------------|
| 20 | FTP | **File Transfer Protocol (Data)** - The File Transfer protocol provides a mechanism for transferring specific files between network-connected computer systems. The transfer is typically performed using the ftp client. Most modern web browsers can also browse and download files on a remote FTP server. FTP uses TCP (rather than UDP) to transfer files, which is considered a highly reliable transport mechanism. FTP does not encrypt data and is not considered a secure file transfer protocol. Secure Copy Protocol (SCP) and Secure File Transfer Protocol (SFTP) are strongly recommended in place of FTP. |
| 21 | FTP | **File Transfer (Control)** - Traditionally, FTP has two ports assigned (port 20 and port 21). Port 20 was initially considered the data transfer port, while port 21 was assigned to communicate control information. However, in modern implementations, port 20 is rarely used, with all communication taking place on port 21. |