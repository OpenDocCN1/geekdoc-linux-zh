Was found on the following hosts:

IP Address: 127.0.0.1        Hostname: Could not resolve hostname

Expand Account Information About Users with Sendmail [Low Risk]

EXPN allows an intruder to determine if an account exists on a system, providing a significant aid to a brute force attack on user accounts.

If you are running Sendmail, add the line “O:noexpn” to your Sendmail configuration file, usually located in /etc/sendmail.cf. With other mail servers, contact your vendor for information on how to disable the verify command.

Was found on the following hosts:

IP Address: 127.0.0.1        Hostname: Could not resolve hostname

Trace Routing of Packets [Low Risk]

Traceroute allows you to determine the path a packet takes between two hosts. This information allows someone to determine network topology and routers on the network.

Was found on the following hosts:

IP Address: 127.0.0.1        Hostname: Could not resolve hostname

127.0.0.1

0

--------- End of Report ---------

Listing 9-5 displays the trusted hosts – those that don’t need password authentication to log in to your system. In effect, your host might as well have the same type of security as the trusted hosts – which may seem convenient at first, but can be a real security problem. From the standpoint of security, the results of this scan were good because they show no trusted hosts.

Listing 9-5: Trusted hosts

```
Internet Security Scanner (C) 1992-1997
ISS SAFEsuite Version 4.3.8
By Internet Security Systems, Inc.
Analysis Report
```

Host Inventory

Summary Information

Hosts Scanned: 1

Hosts with Active Services: 1