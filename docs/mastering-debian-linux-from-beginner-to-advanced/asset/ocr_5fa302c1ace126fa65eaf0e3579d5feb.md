+   5. Allow traffic from a specific IP address:

```
`sudo ufw allow from 192.168.1.100`
```

+   6. Delete a rule:

```
`sudo ufw delete allow 22/tcp`
```

# Configuring UFW

Here's an example of a basic UFW configuration that allows SSH and HTTP traffic while blocking all other incoming connections:

```
```
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw enable
```
```

# IPTables

IPTables is a powerful firewall tool that provides fine-grained control over network traffic. While it's more complex than UFW, it offers greater