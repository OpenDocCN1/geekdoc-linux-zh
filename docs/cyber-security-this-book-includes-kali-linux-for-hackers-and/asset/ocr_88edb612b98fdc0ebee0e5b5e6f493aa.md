progress. This documentation can be located on the following page: http://docs.kali.org/

# Kali Linux Tools

Kali Linux contains a large number of tools obtained from different sources related to the field of security and forensics.

A list of all these tools and a quick reference for them are provided on the following website: http://tools.kali.org/

# Shell Scripting

The Shell Bash allows you to automate an action or perform repetitive tasks that consume a great deal of time. For the following practice, a website that publishes lists of proxies will be used.

Using commands from the bash shell, the IP addresses and Ports of the Proxies will be extracted to a file.

```
# wget http://www.us-proxy.org/
# grep "<tr> <td>" index.html | cut -d ">" -f 3,5 | cut -d "<" -f 1,2 | sed 's / \\/ td> /: / g'
```

# Capture Information

This phase attempts to collect as much information as possible about the objective, such as possible usernames, IP addresses, name servers, and other relevant information. During this phase, each piece of information obtained is important and should not be underestimated. Bear in mind that the collection of a greater amount of information will generate a greater probability for a satisfactory attack.

The process where information is captured can be divided in two ways - the capture of active information and the capture of passive information. In the first way, information is collected by sending traffic to the target network, such as performing ICMP ping, and TCP / UDP port scans. For the second case, information is obtained on the target network using third-party services or sources, such as Google, Bing, or social networks.

# Public Sources