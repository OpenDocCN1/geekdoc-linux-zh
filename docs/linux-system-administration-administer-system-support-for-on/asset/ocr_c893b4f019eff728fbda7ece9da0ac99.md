TABLE 11-3 NETWORK CLASSES IN IP
| Class | Initial Octet | Network Addresses | Host Addresses |
| :--- | :--- | :--- | :--- |
| A | 1-126 | aaa | bbb.ccc.ddd |
| B | 128-191 | aaa.bbb | ccc.ddd |
| C | 192-224 | aaa.bbb.ccc | ddd |
| Reserved | 0, 127, 224-254* | n/a | n/a |

> *Zero is not used, and 127 is used for the loopback address. 224-254 is reserved for other network uses including broadcasting.*

As Table 11-3 illustrates, the numbers in the first part of a network address (the initial octet that corresponds to aaa) fall within a range that immediately reveals the network’s class. (Well, maybe not immediately, but certainly with practice.) So, quick quiz: Address 124.228.8.4 is in what class of network? (The answer is Class A.) The bad news is, this topic can get much more complex in a hurry; the good news is, not right now.

# Naming Your Networks with DNS

Most users don’t want to have to memorize numbers simply to get to another host on a network – and having to type numbers is almost as tedious for some. Instead of typing 128.227.8.4, for example, you could have typed maple.circa.ufl.edu. Such address names use the Domain Name Service (DNS) when you open a Web browser. For example, www.yahoo.com is the name that associates with any of several different IP addresses, depending on the network traffic.

The DNS naming convention works in a manner similar to that of the UNIX file-system structure. You begin with a root nameserver (.), and from there, decide whether the address you’re sending to is government (.gov), commercial (.com), nonprofit organization (.org), network service provider (.net), or part of another country. All these designations are called top-level domains. Table 11-4 lists top-level domains for countries.