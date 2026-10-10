**What is the difference between using nmap localhost on our computer and nmap [ip of our host] from another host?**
>> The firewall. Apparently, nmap localhost does not take into account the firewall and takes the open ports as such, while if we try to access from another computer the open ports that appeared in the first case in the second appear filtered to us.

**What happens if we use the -p “**” option (eg nmap -p “**” scanme.nmap.org )? What are the advantages and disadvantages?**
>> All ports of the referenced host (s) would be analyzed. The advantage is that each and every TCP port of the target host (s), which could be 65535 ports, is analyzed. The main disadvantage is the response time (By default it only scans 1000 most common ports)

**What would happen if we instead executed the -F option? What advantages and disadvantages does it present?**
>> -F requests a Fast Scan, in which only the 100 most used ports, would be scanned.
The opposite would happen that in the previous question, it is a very fast scanner but it covers many fewer ports.

**To which set of commands would an aggressive survey (nmap -A) be equivalent?**
>> Aggressive polling is equivalent to the Operating System (-O), version (-sV), script scanner (-sC) and traceroute (- traceroute) scanning, all at once.

**Does an ARP scan work outside our intranet?**
>> No

**Is there a limit to the number of options we can execute in a nmap scan?**
>> Although we can use almost any option to our liking, there are some combinations that are not valid, in most cases because they are contradictory.