# 25.4 Routing

The IT, Dev, and Admin networks are not directly routable from the public student network but the public student network is routable from all other networks. You will need to use various techniques covered in the course to gain access to the other networks. For example, you may need to exploit machines NAT’d behind firewalls, leveraging dual-homed hosts or client-side exploits.

# 25.5 Machine Ordering & Attack Vectors

The IP addresses of the lab machines are not significant. For example, you do not need to start with 10.11.1.1 and work your way through the machines in numerical order. One of the most important skills you will need to learn as a penetration tester is how to scan a number of machines in order to find the lowest-hanging fruit. Also, keep in mind that you may not be able to fully compromise a particular network without first moving into another.

# 25.6 Firewall / Routers / NAT

The firewalls and other networking devices that connect the networks together are not directly exploitable. Although they are in scope and you may attempt to gain access to them, they are not intentionally created for you to do so. In addition, lengthy attacks such as bruteforcing or DOS/DDOS are highly discouraged as they will render the firewalls, along with any additional networks connected to them, inaccessible to you and other students.

A number of machines in the labs have software firewalls enabled and may not respond to ICMP echo requests. If an IP address does not respond to ICMP echo requests, this does not necessarily mean that the target machine is down or does not exist.

# 25.7 Passwords

Spending an excessive amount of time cracking the root or administrator passwords of all machines in the lab is not required. If you have tried all of the available wordlists in Kali, and used information gathered throughout the labs, stop and consider a different attack vector. If you have significant cracking hardware, then feel free to continue on to crack as many passwords as you can.

# 25.8 Wrapping Up

If you’ve taken the time to understand the course material presented in the course book and associated videos and have tackled all the exercises (including the “extra mile” exercises), you’ll enjoy the full lab assessment. If you’re having trouble, consider filling in knowledge gaps in the course material, and if you’re still stuck, step back and take on new perspective. It’s easy to get so fixated on a single challenge and lose sight of the fact that there may be a simpler solution waiting down a different path. Take good notes and review them often, searching for alternate paths that might advance your assessment. When all else fails, do not hesitate to reach out to the student administrators. Finally, remember that you often have all the knowledge you need to tackle the problem in front of you. Don’t give up, and remember the “Try Harder” discipline!