encrypted management for the sensitive communication. Furthermore, any attacker can download the client version of these applications and attempt to connect to the application's agent with a captured or guessed username and password. This assumes that there is no separate management network that the attacker cannot access, which prevents him or her from connecting to any agents. While separate management networks are ideal for safe and secure management, implementation of out-of-band management networks is not only very costly but adds a significant amount of complexity to a network.

SSH can be used as a secure management alternative by providing encrypted communication for any type of system or device management. Not only does SSH provide secure communication for remote command line management, which is the most popular management method on most Unix systems; it provides secure communication of graphic user interfaces (GUIs) with less secure applications such as VNC. In addition, SSH can provide two-factor authentication for all management methods by requiring a public key and password for management access. As best practice, two-factor authentication should be used for all management methods, as it reduces the number of brute-force attacks, password-guessing attacks, and dependencies on passwords for security. SSH can enforce two-factor authentication quite easily, which supports a critical best practice in management security. Lastly, SSH can eliminate the need for an out-of-band management network, removing a significant amount of cost and adding administrative simplicity in managing the systems and devices. The following list describes the advantages of using SSH for management:

+   ■ Encrypted management
+   ■ Encrypted GUI management with port forwarding (discussed further in Chapter 6)
+   ■ Significant cost savings
+   ■ Elimination of separate out-of-band management networks
+   ■ Added simplicity
+   ■ Two-factor authentication

# Proxy Services

SSH can also be used to secure proxy services. Proxy servers have been identified to contain established benefits to which SSH can add value. Deploying SSH as a proxy service to access remote systems, devices, and applications in a safe and easy manner is one of the strongest, but most unused, benefits of SSH. SSH proxies can work with traditional proxy services such as SOCKS in order to secure the application from end to end. A SOCKS server can be set up in an