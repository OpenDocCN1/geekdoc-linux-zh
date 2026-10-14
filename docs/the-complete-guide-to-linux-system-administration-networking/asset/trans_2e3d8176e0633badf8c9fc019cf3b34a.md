

# Project 15-5

In this project, you set up and test a caching name server using the standard packages provided with Red Hat Linux and Fedora. To complete this project, you should have Fedora installed, with networking established, root access to the system, and an Internet connection.

- 1. Log in to Linux, open a command-line window, and change to root access.
- 2. Check that the necessary packages are installed using the following commands:
  `rpm -q bind`
  `rpm -q bind-utils`
  `rpm -q caching-nameserver`

You will probably need to install the last package from Fedora CD 3 using this command (after mounting the CD and changing to the appropriate directory):

```
rpm -Uvh caching-nameserver*
```

- 3. Start the name server:
  `service named start`

2. Also on the server, edit the /etc/hosts.deny file by adding this line:
`portmap client_host`

3. What steps need to be taken to activate these two changes?

4. On the client, log in as root and create a mount point directory for the NFS server. Here is an example:
`mkdir /mnt/server_hostname`

5. Edit the /etc/fstab file on the client by adding this line:
`server_hostname:/usr/share/doc /mnt/server_hostname nfs o=ro,rsize=8192,wsize=8192 0 0`

6. Use the mount command on the client to mount the NFS file system you exported:
`mount /mnt/server_hostname`
Why did it not work?

7. On the server, edit /etc/hosts.deny, removing your addition.

8. On the client, try the mount command again.

9. Change to the mount point directory that you created.

10. Noting that the directory is exported as rw on the server, create a new directory in that directory:
`mkdir mydocs`

11. Give three reasons why this didn't work. Log off.

![](img/43f64015de86d989e30eff5bb284fb96_775_0.png)

4. Use this command to query for a domain name. You have not changed your /etc/resolv.conf file, so your previously configured DNS server can still be used.

```
dig www.sony.com
```

5. Notice the Query time and SERVER lines in the last part of the output of dig.

6. Now, try out your caching name server with this command:

```
dig @localhost www.sony.com
```

7. Notice the same two lines at the end of the output. How do they differ? Why was the time not faster when the response was already cached at your preconfigured name server?

8. Open the /etc/named.conf file in a text editor.

9. Within the options section near the top of the file, right after the line directory "/var/named", insert the following lines. Substitute the IP address of your primary DNS name server at your ISP for the IP address shown here:

```
forward first;
forwarders {
    198.60.22.2;
};
```

10. Save the file and exit the editor.

11. Run the named-checkconf command to see whether any syntax errors were introduced as you edited the configuration file. If so, correct them.

12. Reload the configuration using this command (you may see a warning message about the name key, which you can safely ignore for this project):

```
rndc reload
```

13. Select another domain name for testing. You should select one that others in your class have not selected and that you would not expect to have been visited often; a somewhat obscure domain name is better for this test. Use dig with your localhost to query for the domain you selected:

```
dig @localhost www.cern.org
```

14. Notice how long the query time is, given near the end of dig’s response.

15. Perform the same query again. How does the query time differ? From where is the information being taken? What advantage does forwarding have over simply using a caching name server?

16. If you wish, you can have your system always use the local DNS server (the daemon running on the same computer) for name resolution. To do this, edit your /etc/resolv.conf file to contain only this line (plus any comment lines you choose to include):

```
nameserver 127.0.0.1
```

# Project 15-6

In this project, you check the contents of remote name servers using the dig command. To complete this project, you should have Linux installed (any version that includes the dig utility), with networking established, and an Internet connection.

Sometimes the results you receive from a name resolution are unexpected. This can be caused by several problems, such as a poorly configured DNS server, a DNS server without a slave that temporarily goes down, or slow propagation of a change in a DNS file. In this project, you query step by step through several name servers to get a complete name resolution. This project uses the sample domain name ftp.hq.nasa.gov, but feel free to experiment on any domain name you choose once you understand the process being illustrated.

- 1. Log in to Linux, open a command-line window, and change to root access.
- 2. Query your ISP's name server for the address you want to find. Instruct the DNS server not to search "down the tree," but to give you only the first piece of information that it has, using the "norecurse" option (to stop recursion) to arrive at the requested domain:
  
  `dig ftp.hq.nasa.gov NS +norecurse`

- 3. The result is a list of the addresses of authoritative DNS servers for the .gov domain, unless the server you queried happens to have cached the authoritative servers for nasa.gov as well. In that case, you might choose to use this command to get the .gov NS records specifically:
  
  `dig gov NS +norecurse`

- 4. The dig command shows a list of name servers that manage the .gov top-level domain. From that list of servers, choose any three and write them down.

- 5. To each of those three name servers, make the following query to check the next part of the domain:
  
  `dig @gov-ns-server nasa.gov NS +norecurse`

7. If so, continue as follows. Execute the command below. Where you see nasa-ns-server below, insert one of the server names that you wrote down in Step 6 from the output of the three commands you executed in Step 5. (Many domains do not have three name servers, but NASA has a huge network and so includes numerous name servers.)

```
dig @nasa-ns-server hq.nasa.gov NS +norecurse
```

8. The output of the dig command you executed in Step 7 shows you a list of name servers that have information about hq.nasa.gov servers. Each of the name servers is listed with an "NS" after it. One of the name servers listed is probably mx.ns1.nasa.gov (though these name servers can change over time within an organization). Query that name server, or one of the others listed with "NS" in the output of Step 7 using this dig command (substitute a different name server for mx.ns1.nasa.gov if you choose to try a different name server):

```
dig @mx.ns1.nasa.gov ftp.hq.nasa.gov
```

Below is the output from the above command. The exact output that you see may differ.

```
; <<>> DiG 9.1.3 <<>> @mx.ns1.nasa.gov ftp.hq.nasa.gov
;; global options: printcmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 49505
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1,
;; AUTHORITY: 4, ADDITIONAL: 4

;; QUESTION SECTION:
;ftp.hq.nasa.gov. IN A

;; ANSWER SECTION:
ftp.hq.nasa.gov. 86400 IN A 198.116.65.46

;; AUTHORITY SECTION:
hq.nasa.gov. 86400 IN NS ns3.hq.nasa.gov.
hq.nasa.gov. 86400 IN NS mx.ns1.nasa.gov.
hq.nasa.gov. 86400 IN NS ns1.hq.nasa.gov.
hq.nasa.gov. 86400 IN NS ns2.hq.nasa.gov.

;; ADDITIONAL SECTION:
ns3.hq.nasa.gov. 86400 IN A 198.116.65.241
mx.ns1.nasa.gov. 3600 IN A 128.102.18.31
ns1.hq.nasa.gov. 86400 IN A 131.182.230.28
ns2.hq.nasa.gov. 86400 IN A 131.182.1.28

;; Query time: 290 msec
;; SERVER: 128.102.18.31#53(mx.ns1.nasa.gov)
;; WHEN: Tue Apr 23 22:09:43 2002
;; MSG SIZE rcvd: 188
```

9. Look at the SERVER line, third from the bottom. This identifies which name server responded to the query. See if you can locate this address in the ADDITIONAL section.

What is the host name of the responding name server?

10. Look in the AUTHORITY section. Is the responding name server listed as being authoritative for the hq.nasa.gov domain?

What does this process tell you about the quality of the information you just obtained? How could you use this process if you were seeing unexpected results from standard DNS operations?

11. Log off.

# Project 15-7

In this project, you experiment with e-mail aliases and sendmail. To complete this project, you should have Linux installed, with root access to the system. For simplicity's sake, the directory names referred to are specific to Red Hat Linux and Fedora, but most distributions should use the same location for the files named.

- 1. Log in to Linux, open a command-line window, and change to root access.
- 2. View the mail log using this command (this will occupy this text window for the duration of this project):
  ```
  tail -f /var/log/maillog
  ```
- 3. Use a text editor to add the following lines to the end of the /etc/aliases file:
  ```
  supervisor:root
  spam:/tmp/spamcan
  ```
- 4. Save the file, then execute the following command:
  ```
  newaliases
  ```
- 5. Use a mail program to send a message to the address "supervisor". The following command is one way to do this, sending the contents of a text file as the body of the message:
  ```
  mail -s "testing aliases" supervisor < /etc/syslog.conf
  ```
- 6. Watch the window where the maillog is displayed. When you see a line indicating that your message has been delivered, open an e-mail reading program to see that the message addressed to supervisor was delivered to root.
- 7. Send another e-mail message to spam. An example command to do this is shown here:
  ```
  mail -s "still testing aliases" spam </etc/syslog.conf
  ```
- 8. Watch the window where the maillog is displayed to see when the message has been delivered by sendmail.

