# 434 Linux Administration: A Beginner's Guide

grouped by predefined categories or channels; for example, there are categories for security-related logs, a general category, a resolver category, a queries category, and so on.

Unfortunately, the configurability of this logging statement comes at the price of some additional complexity, but the default setting up by named is good enough for most users. Here is a simple logging directive example:

+   1. logging {
2. category default { default_syslog };
3. category queries { default_syslog };
4. 
5. };

> NOTE Line numbers have been added to the preceding listing to add readability.

The preceding logging specification means that all logs that fall under the default will be sent to the system's syslog (the default category defines the logging options for categories where no specific configuration has been defined).
Line 3 in the listing where all queries will be logged to; in this case, all queries will be logged to the system syslog.

The server Statement The server statement tells BIND specific information about other name servers it may be dealing with. The format of the server statement is follows:

+   1. server ip-address {
2. bogus yes/no;
3. keys { string; [string; ...] };
4. transfer-format one-answer/many-answers;
5. <other options>...
6. };

Here, ip-address in line 1 is the IPv4 or IPv6 address of the remote server in question.
The Bogus option in line 2 is useful if you are dealing with another site that may be sending you information about a misconfiguration. The keys clause in line 3 specifies a key_id defined by the key statement, which can be used to secure transactions talking to the remote server. This key is used in generating a request signature that is appended to messages exchanged with the remote name server. In line 4, transfer-format, tells BIND whether the remote name server can accept multiple answers in a single query response.