![](bbox=[0.215, 0.096, 0.918, 0.313])

**Figure 6.25**  
Using `set q = any` to see all possible DNS information for a given host or domain.

Using the `set q = value` command (or query) is another way to extract information from DNS using `nslookup`. While there are many different types of queries, knowing a few can help you gather important information quickly. Using the `set q = soa` query in nslookup will give you the SOA information for a given domain, as seen in Figure 6.23.

Another useful feature is the ability to determine the mail exchanger (MX) values for a given system. This is highly useful when debugging SMTP problems. Using the `set q = mx` query, as in Figure 6.24, you will see the MX values for the domain or host, as well as the preference values.

Finally, if you're not quite sure what information you are looking for, you can generate a query to give you as much information as is available by using the `set q = any` query, as shown in Figure 6.25.

`nslookup` allows users to contact DNS servers for information about various hosts and domains.

# WINS Overview

Windows 2000 provides the ability to map NetBIOS names to IP addresses using WINS servers. WINS stands for Windows Internet Name Service. The unique aspect of WINS, as compared to DNS, is that each client machine registers its own name and IP address with the server. This provides the ability to implement an (almost) hands-off name resolution service. WINS can be used (and it is recommended to do so) to replace the functionality of the local LMHOSTS file.