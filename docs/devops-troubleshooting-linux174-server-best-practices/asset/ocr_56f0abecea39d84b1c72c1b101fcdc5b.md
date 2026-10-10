```
Interesting ports on web1 (10.1.2.5):  
PORT STATE SERVICE
80/tcp filtered http
```

Aha! nmap is smart enough that it can often tell the difference between a closed port that is truly closed and a closed port behind a firewall. Now normally when a port is actually down, nmap will report it as closed. Here it reported it as filtered. What this tells us is that there is some firewall in the way that is dropping the packets to the floor. This means you need to investigate any firewall rules on the gateway (10.1.1.1) and on web1 itself to see if port 80 is being blocked.

# Test the Remote Host Locally

At this point, we have either been able to narrow the problem down to a network issue or we believe the problem is on the host itself. If we think the problem is on the host itself, we can do a few things to test whether port 80 is available.

Test for Listening Ports Once you are satisfied that the problem is not on you network, you should log in to the web server and test whether port 80 is listening. The netstat -lnp command will list all ports that are listening along with the process that has the port open. You could just run that and parse through the output for anything that is listening on port 80, or you could use grep to see only the things that are listening on port 80:

```
$ sudo netstat -lnp | grep :80
tcp 0 0 0.0.0.0:80 0.0.0.0:* LISTEN 919/apache
```

The first column tells you what protocol the port is using. The second and third columns are the receive and send queues (both set to 0 here). The column you want to pay attention to is the fourth column, as it lists the local address on which the host is listening. Here the 0.0.0.0:80 tells us that the host is listening on all of its IPs for port 80 traffic. If Apache were listening only on the server’s Ethernet address, you would see a specific IP like 10.1.2.5:80 here.