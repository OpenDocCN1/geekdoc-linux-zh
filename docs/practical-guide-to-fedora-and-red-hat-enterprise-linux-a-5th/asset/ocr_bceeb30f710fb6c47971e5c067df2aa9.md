by a NEWLINE (press RETURN in a text editor). When you insert the NEWLINE before
or after a SPACE, you can indent the following line to make it easier to read.
Do not break lines in this manner while editing on a Windows machine, as
the NEWLINES may not be properly escaped (Windows uses RETURN-LINEFEEDs to
end lines).

Configuration files that do not follow these conventions are noted in the text.

# SPECIFYING CLIENTS

Table 11-3 shows some common ways to specify a host or a subnet. Most of the
time you can specify multiple hosts or subnets by separating the host or subnet spec-
ifications with SPACES.

Table 11-3 Specifying a client

| Client name pattern | Matches |
| :--- | :--- |
| n.n.n.n | One IP address. |
| name | One hostname, either local or remote. |
| Name that starts with . | Matches a hostname that ends with the specified string. For<br>example, .tcorp.com matches the systems kudos.tcorp.com<br>and speedy.tcorp.com, among others. |
| IP address that ends with . | Matches a host address that starts with the specified numbers.<br>For example, 192.168.0. matches 192.168.0.  –<br>192.168.0.255. If you omit the trailing period, this format does<br>not work. |
| Starts with @ | Specifies a netgroup. |
| n.n.n.n/n.m.m.m or<br>n.n.n.n/mm | An IP address and subnet mask specify a subnet. |
| Starts with / | An absolute pathname of a file containing one or more names<br>or addresses as specified in this table. |
| **Wildcard** | **Matches** |
| * and ? | Matches one (?) or more (*) characters in a simple hostname<br>or IP address. These wildcards do not match periods in a<br>domain name. |
| ALL | Always matches. |
| LOCAL | Matches any hostname that does not contain a period. |
| **Operator** |  |
| EXCEPT | Matches anything in the preceding list that is not in the follow-
|  | ing list. For example, a b c d EXCEPT c matches a, b, and d. |
|  | Thus you could use 192.168. EXCEPT 192.168.0.1 to match all<br>IP addresses that start with 192.168. except 192.168.0.1. |