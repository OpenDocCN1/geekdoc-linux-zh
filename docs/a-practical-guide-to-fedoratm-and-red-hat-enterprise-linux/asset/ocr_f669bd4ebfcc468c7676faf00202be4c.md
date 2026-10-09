# SETTING UP DIFFERENT TYPES OF DNS SERVERS

order of the View classes, all users—including local users—would get the view intended for the public and no users would see the local view.

Many statements from the Options clause can be used within View clauses, where they override statements in the (global) Options clause. The **recursion** statement, which can appear within an Options clause, appears in each View clause. This **named.conf** file sets up a server that provides recursive answers to queries that originate locally and iterative answers to queries from the public. This setup provides quick, complete answers to local users, limiting the network and processor bandwidth that is devoted to other users while continuing to provide authoritative name service for the local servers.

To make **named.conf** easier to understand and maintain, zones in different View clauses can have the same name but different zone files. Both the local and public View clauses in the example have zones named **zach.net**. The public **zach.net** zone file is named **public.net** and the local one is named **local.net**.

The Logging clause is described on page 887.

The zone files defining **zach.net** are similar to the ones in the previous examples; the public file is a subset of the local one. Following the SOA resource record in both files is a TXT, two NS, and two MX resource records. Next are three CNAME resource records that direct queries addressed to www.zach.net, ftp.zach.net, and mail.zach.net to the system named **ns.zach.net**. The next four resource records specify two nameserver addresses and two mail servers for the ns.zach.net domain.

The final four resource records appear in the local **zach.net** zone file and not in the public zone file; they are address (A) resource records for local systems. Instead of keeping this information in /etc/hosts files on each system, you can keep it on the DNS server, where it can be updated easily. When you use DNS instead of /etc/hosts, you must change the **hosts** line in /etc/nsswitch.conf (page 495) accordingly.

```
$ cat local.net ; zach.net local zone file ; $TTL 3D @ IN SOA ns.zach.net. mgs@sobell.com. ( 201311118 ; serial 8H ; refresh 2H ; retry 4W ; expire 1D ) ; minimum IN TXT "Sobell Associates Inc." IN NS ns ; Nameserver address (unqualified) IN NS ns.speedy.net. ; Nameserver address (qualified) IN MX 10 mail ; Mail exchange (primary/unqualified) IN MX 20 mail.max.net. ; Mail exchange (2nd/qualified)
```