single connection with MaxAuthTries. The default is 6.

```
MaxAuthTries 6
```

After half of a user’s permitted attempts in a single session have failed, sshd logs further failures. Authentication attempts include both public key authentication and passwords. After MaxAuthTries failures, the user must initiate a new SSH session and try again.

My usual failure procedure is to fail to log in six times, then remember that I have a different username on this machine. When I take my own advice on changing usernames from Chapter 5, “SSH Clients,” and install my public key everywhere as in Chapter 7, “SSH Keys,” this problem goes away.

# Verify Login Attempts against DNS

A log message like “Login failed from boss’s computer” makes you sigh. A log message like “Login succeeded from Hacker Haven Nation” should trigger alarm. The owner of an IP address controls the reverse DNS for that address. An intruder who controls the reverse DNS for his IP address can change the apparent hostname to something within your company. For protection against this sort of attack, sshd can verify connection attempts against forward DNS entries.

```
UseDNS no
```

When set to yes, every time a client connects, sshd looks up the host name for the source IP, and then looks up the IP address for the host name. If the DNS names don’t match, sshd rejects the connection.

Suppose an intruder controls the reverse DNS for his IP address 192.0.2.99. He gives it a hostname within your organization, such as dhcp12.mwl.io, and connects to your SSH server. Your SSH server asks its DNS server for the IP address for dhcp12.mwl.io. If that DNS entry doesn’t exist, or it points to an IP other than 192.0.2.99, sshd rejects the connection.

If DNS fails, sshd waits for a full DNS timeout before allowing the connection.

UseDNS requires that your DNS be tidy, coherent, and correct. While I’m in favor of auditing an organization’s DNS entries, performing such audits via UseDNS lacks elegance. DNS checks don’t help if an intruder can poison the server’s DNS cache. If you’re a home user, your ISP probably controls the reverse DNS on your connection. Also, DNS checks can increase system load. If you serve hundreds or thousands of simultaneous SSH users, that load can be substantial. When DNS fails, failed DNS checks will slow down all SSH logins. Finally, many IPv6 sites haven’t configured reverse DNS and won’t for the foreseeable future.

I discourage enabling UseDNS.