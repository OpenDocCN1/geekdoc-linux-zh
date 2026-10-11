
- netmask: The subnet mask
- gateway: The IP address of your router or default gateway
- dns-nameservers: The IP addresses of the DNS servers you want to use

### Configuring DNS

DNS (Domain Name System) resolution can be configured in two main ways:

1. In the `/etc/network/interfaces` file (as shown above)
2. In the `/etc/resolv.conf` file

#### Using /etc/resolv.conf

The `/etc/resolv.conf` file is used to configure the system's DNS resolver. Here's an example configuration:

```
nameserver 8.8.8.8
nameserver 8.8.4.4
```

However, be aware that this file may be overwritten by DHCP or other network management tools. For a more permanent solution, you can use the `resolvconf` package or Network Manager.

### Using Network Manager

If you're using a desktop environment, you might prefer to use Network Manager for easier network configuration. Network Manager provides a graphical interface for managing network connections and can be configured to handle static IP and DNS settings.

To configure a static IP using Network Manager:

1. Click on the Network Manager icon in the system tray
2. Select "Edit Connections"
3. Choose the connection you want to modify
4. Go to the "IPv4 Settings" tab
5. Change the method to "Manual"
6. Add your static IP address, netmask, and gateway
7. In the DNS servers field, enter your preferred DNS server IP addresses

## Network Troubleshooting

Network issues can be frustrating, but Debian provides several tools to help diagnose and resolve these problems.

### Ping

The `ping` command is used to test network connectivity between your computer and another network device or website.

```
ping google.com
```

This command sends ICMP echo request packets to the specified host and waits for a reply. If successful, you'll see a series of responses with round-trip times.

### Traceroute

The `traceroute` command shows the path that packets take to reach a destination, helping you identify where network issues might be occurring.

```
traceroute google.com
```

This command will display a list of routers (hops) that the packets traverse to reach the destination.

### Netstat

The `netstat` command provides information about network connections, routing tables, and network interface statistics.

```
netstat -tuln
```

This command shows all active TCP and UDP connections, along with the ports they're using.

### IP Command

The `ip` command is a powerful tool for viewing and manipulating network configuration.

To view IP addresses:

```
ip addr show
```

To view routing information:

```
ip route show
```

### Checking DNS Resolution

To check if DNS resolution is working correctly, you can use the `nslookup` or `dig` commands:

```
nslookup google.com
```

or

```
dig google.com
```

These commands will show you the IP addresses associated with the domain name.

### Checking Network Interface Status

To check the status of your network interfaces:

```
ip link show
```

This command will display all network interfaces and their current state (UP or DOWN).

### Firewall Troubleshooting

If you're having issues with network connectivity, it's worth checking if the firewall is blocking traffic. In Debian, the default firewall is `iptables`. You can list the current firewall rules with:

```
sudo iptables -L
```

If you're using `ufw` (Uncomplicated Firewall), you can check its status with:

```
sudo ufw status
```

### Checking Network Services

To see which network services are running and listening for connections:

```
sudo ss -tuln
```

This command shows all TCP and UDP ports that are in a listening state.

### Logging

Network-related logs can be found in various files under the `/var/log/` directory. Some important log files to check include:

- `/var/log/syslog`: General system logs, including network-related messages
- `/var/log/kern.log`: Kernel logs, which may include network driver issues
- `/var/log/auth.log`: Authentication logs, useful for troubleshooting SSH connection issues

You can use the `tail` command to view the most recent entries in these log files:

```
sudo tail -f /var/log/syslog
```

## Setting up a Basic Web Server

Debian makes it easy to set up a basic web server using popular software like Apache or Nginx. We'll cover the installation and basic configuration of both.

### Apache Web Server

Apache is one of the most widely used web servers and is included in the Debian repositories.

#### Installation

To install Apache:

```
sudo apt update
sudo apt install apache2
```

#### Basic Configuration

The main configuration file for Apache is `/etc/apache2/apache2.conf`. However, for most basic setups, you won't need to modify this file directly.

Apache's configuration in Debian is modular, with configuration files split into several directories:

- `/etc/apache2/mods-available/`: Available Apache modules
- `/etc/apache2/mods-enabled/`: Enabled Apache modules
- `/etc/apache2/sites-available/`: Available virtual host configurations
- `/etc/apache2/sites-enabled/`: Enabled virtual host configurations

#### Creating a Virtual Host

To create a new virtual host:

1. Create a new configuration file in `/etc/apache2/sites-available/`:

```
sudo nano /etc/apache2/sites-available/mysite.conf
```

2. Add the following configuration (adjust as needed):

```
<VirtualHost *:80>
    ServerName mysite.com
    ServerAlias www.mysite.com
    DocumentRoot /var/www/mysite
    ErrorLog ${APACHE_LOG_DIR}/mysite_error.log
    CustomLog ${APACHE_LOG_DIR}/mysite_access.log combined
</VirtualHost>
```

3. Create the document root directory:

```
sudo mkdir -p /var/www/mysite
```

4. Enable the virtual host:

```
sudo a2ensite mysite.conf
```

5. Reload Apache:

```
sudo systemctl reload apache2
```

### Testing Apache

After installation, Apache should start automatically. You can check its status with:

```
sudo systemctl status apache2
```

To test if Apache is serving pages, open a web browser and navigate to `http://localhost` or your server's IP address. You should see the default Apache page.

## Nginx Web Server

Nginx is known for its high performance and low resource usage, making it a popular choice for web servers.

### Installation

To install Nginx:

```
sudo apt update
sudo apt install nginx
```

### Basic Configuration

The main configuration file for Nginx is `/etc/nginx/nginx.conf`. Like Apache, Nginx uses a modular configuration approach in Debian.

Important directories include:

- `/etc/nginx/conf.d/`: Additional configuration files
- `/etc/nginx/sites-available/`: Available virtual host configurations
- `/etc/nginx/sites-enabled/`: Enabled virtual host configurations

### Creating a Virtual Host

To create a new virtual host:

1. Create a new configuration file in `/etc/nginx/sites-available/`:

```
sudo nano /etc/nginx/sites-available/mysite
```

2. Add the following configuration (adjust as needed):

```
server {
    listen 80;
    server_name mysite.com www.mysite.com;
    root /var/www/mysite;
    index index.html index.htm;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

3. Create the document root directory:

```
sudo mkdir -p /var/www/mysite
```

4. Enable the virtual host by creating a symbolic link:

```
sudo ln -s /etc/nginx/sites-available/mysite /etc/nginx/sites-enabled/
```

5. Test the Nginx configuration:

```
sudo nginx -t
```

6. If the test is successful, reload Nginx:

```
sudo systemctl reload nginx
```

### Testing Nginx

After installation, Nginx should start automatically. You can check its status with:

```
sudo systemctl status nginx
```

To test if Nginx is serving pages, open a web browser and navigate to http://localhost or your server's IP address. You should see the default Nginx welcome page.

## Introduction to Secure FTP and SSH

Secure communication is crucial for remote server management and file transfers. Two commonly used protocols for these purposes are SFTP (Secure File Transfer Protocol) and SSH (Secure Shell).

## Secure FTP (SFTP)
