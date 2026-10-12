before starting the service, it consults the /etc/hosts.allow file to see if the host requesting service is allowed that service. If nothing appears in /etc/hosts.allow about that host, TCP wrapper checks the /etc/hosts.deny file to see if it should deny the service. If both files are empty, TCP wrapper allows the host to access the requested service.

You can place the line ALL:ALL in the /etc/hosts.deny file to deny all hosts access to any Internet services on your system. Then you can add to /etc/hosts.allow the names of those hosts that can access services on your system. For example, to allow only hosts from the 192.168.1.0 network to access services on your system, place the following line in the /etc/hosts.allow file:

```
ALL: 192.168.1.0/255.255.255.0
```

If you want to permit access to a specific Internet service to a specific remote host, you can do so using the following syntax for a line:

```
server_program_name: hosts
```

Here server_program_name is the name of the server program (for example, in.telnetd for TELNET and in.ftpd for FTP), and hosts is a comma-separated list of hosts allowed to access the service. hosts can also take the form of a network address or an entire domain name such as .mycompany.com. For example, here’s how you can allow TELNET access to all systems in the mycompany.com domain:

```
in.telnetd: .mycompany.com
```

# Monitoring System Security

After you set up your system securely, you have to periodically monitor the log files for any signs of intrusion. You should also periodically check security news to learn about recently discovered weaknesses in any of your system components (such as mail server or Web server). If Red Hat provides an upgrade to fix a security problem, download the new RPM files and install them on your system.

![](bbox=[0.15, 0.78, 0.28, 0.86])

Follow the steps covered in Session 23 to download the new RPM files and install them.