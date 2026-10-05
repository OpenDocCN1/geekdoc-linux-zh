# 19 Tunneling Through Deep Packet Inspection

In this Learning Module, we will cover the following Learning Units:

+   - HTTP Tunneling Theory and Practice
- DNS Tunneling Theory and Practice

Deep packet inspection⁹25 is a technology that's implemented to monitor traffic traffic based on a set of rules. It is most often used on a network perimeter, where it can highlight patterns that are indicative of compromise.

Deep packet inspection devices may be configured to allow only specific transport protocols out of, or across the network. For a network administrator could create a rule that terminates any outbound SSH traffic. If they implemented that rule, all connections that use SSH for transport would fail, including any SSH port redirection and tunneling strategies we had implemented.

Given the variety of restrictions that may be implemented on a network, we need to learn and leverage a number of different tunneling tools and strategies to successfully bypass technologies like deep packet inspection.

In this Module, we'll continue from the previous Port Redirection and SSH Tunneling Module, leveraging many concepts we introduced. Most students should complete that Module before beginning this one.

# 19.1 HTTP Tunneling Theory and Practice

This Learning Unit covers the following Learning Objectives:

+   - Learn about HTTP tunneling
- Perform HTTP tunneling with Chisel

In this Learning Unit we will explore the concept of HTTP tunneling, as well as how to perform it with a tool called chisel.

# 19.1.1 HTTP Tunneling Fundamentals

Let's begin our exploration of HTTP tunneling by introducing a simple scenario. In this case, we have compromised CONFLUENCE01, and can execute commands via HTTP requests. However we try to pivot, being blocked by a strictly restrictive network configuration.

Specifically, a Deep Packet Inspection (DPI) solution is now terminating all outbound traffic except HTTP. In addition, inbound ports on CONFLUENCE01 are blocked except TCP/8090. We rely on a reverse shell as it would not conform to the HTTP format and would be terminated at the network perimeter by the DPI solution. We also can't create an SSH remote port forward for the same reason. The only traffic that will reach our Kali machine is HTTP, so we can, for example, make requests with Wget and cURL.