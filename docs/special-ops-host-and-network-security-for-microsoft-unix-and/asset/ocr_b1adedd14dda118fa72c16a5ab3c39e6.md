# Attacking and Defending Microsoft SQL Server • Chapter 12

favorite packet sniffer and start capturing traffic to from your target (assuming you have this level of connectivity). Passwords transmitted over the wire are trivially obfuscated so that a simple game can turn them into plaintext. The password is converted to Unicode and XORed with A5 before being transmitted over the wire. In order to get the plaintext, simply XOR "obfuscated" byte by A5 to produce the original character (you will have to reverse the two hex characters so that 07 becomes 70, for example).

Even if you cannot sniff any accounts on the wire, it may be useful to simply monitor the SQL Server passing over the wire. Assuming no encrypted netlibs are used, it may be possible to get a great deal of information by monitoring the data on the wire. This data can include database names, parameters passed to system stored procedures, usernames, and other sensitive information.

# Brute Forcing Accounts

Another method of gaining access is to pray upon the weak passwords that are frequently used in SQL Server and attack accounts directly. If you are aware or can guess the naming convention for SQL Server accounts, there should be no problem. Assuming that you cannot do this, simply attack the System Administrator account (sa) directly since the account must exist.
Obviously, if the server is in Windows Authentication mode, you'll need to have some operation system context first.

There are several tools for brute forcing accounts. Most all of them involve the use of a dictionary of passwords to compare each user account. Table 12.4 outlines each of the available tools for SQL Server penetration testing that should exist in every toolbox and are best for a given situation.

# Table 12.4 Tools for SQL Server Penetration Testing

| Tool | Author/Company | URL | Description |
|---|---|---|-|
| SQLDict | Arne Vidstrom | [www.security.com/uploads/sqldict.zip](http://www.security.com/uploads/sqldict.zip) | GUI-based password brute-force tool with no instance support |
| SQLhf | Matthew Wagenkne | [www.security.com/uploads/sqlhf.zip](http://www.security.com/uploads/sqlhf.zip) | Command-line brute force tool that can scan networks and supports instances |