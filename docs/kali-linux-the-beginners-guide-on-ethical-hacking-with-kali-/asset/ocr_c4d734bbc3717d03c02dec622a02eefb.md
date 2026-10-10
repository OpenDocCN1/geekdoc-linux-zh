Ncrack’s list of features provides an interface that is very flexible and gives the user full control of the network operations, making it possible to perform brute force attacks that are very sophisticated in nature, providing time templates for easy usage, a runtime interaction that is much like Nmap’s and many other things. Ncrack supports the protocols such as OWA, WinRM, MongoDB, Cassandra, MySQL, MSSQL, PostgreSQL, Redis, SIP, SMB, VNC, POP, IMAP, HTTP and HTTPS, Telnet, FTP, RDP and SSH

# RainbowCrack

RainbowCrack is a general propose Kali Linux tool, which was an implementation of Philippe Oechslin. It is used to crack hashes that have rainbow tables. Rainbow Crack cracks hashes of rainbow tables by making use of the time-memory tradeoff algorithm. This makes it different from hash crackers that are brute force.

A brute force hash cracker will generate all the plaintexts that are possible and then compute the hashes that correspond to the plaintext, all during runtime. It will then compare the hashes that need to be cracked with the hashes in hand. If no match is found even after comparing all available plaintexts, all results of the intermediate computation are discarded.

A time-memory tradeoff hash cracker sets up a stage for pre-computation, and all results of all hashes are stored in a rainbow table. This is a time-consuming computation. But on the first stage of pre-computing is over, hashes that were stored in the rainbow table can be cracked with a performance that is much better and efficient as compared to a brute force cracker.