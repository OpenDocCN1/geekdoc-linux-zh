# Task 6.9: Manage an SSH Server

Unix-like systems have long supported remote access, and Linux is no exception to this rule. Although tools such as Telnet and rlogin are available for remote text-mode access, these protocols are insecure and limited. Today, the Secure Shell (SSH) is the preferred method of providing remote text-mode access to a Linux system. In fact, you can even tunnel an X session through SSH, meaning that an SSH connection will link your local X server to the remote system, enabling you to run X programs remotely. SSH's greatest feature, though, is its built-in encryption. When you use SSH, the risk of your data being intercepted is slim—or more precisely, anybody snooping on your data will find it useless because of SSH's encryption.

# Scenario

Your mail server, configured in Task 6.6, is located in a physically inconvenient site. To enable easier configuration of this system from your desk, you want to configure the SSH server to accept remote logins. To provide the best security, you want to disable direct SSH logins as root, requiring remote users to log in as ordinary users and then, if they require root access, to use su or some other means to acquire superuser privileges. You also want to use SSH's key generation tools to create and use encryption keys as a substitute for ordinary SSH passwords, simplifying the login process.

# Scope of Task

This task requires configuring an SSH server and creating SSH keys for an ordinary user account. Fortunately, most Linux distributions provide reasonable default SSH server configurations, so the first part of this task is fairly simple. SSH key generation is a bit more obscure, but SSH keys are very powerful tools.

# Duration

This task should take half an hour to an hour to complete. Simple changes to SSH server configuration take very little time. You can generate SSH keys very quickly, too, once you know how.

# Setup

You must have both ordinary user and root access to the system you'll be using as an SSH server (mail.panqaee.edu in this example). Presumably you'll do this work at the console, although you could do it via another remote login protocol if one is enabled. If this is a text-mode protocol such as Telnet, disabling this protocol after you've got SSH working will greatly improve the computer's security. You'll also need access as an ordinary user to another system to test the configuration.

If the SSH server package isn't already installed on the computer, install it now. In most cases, it's available in a package called openssh or openssh-server. Major modern Linux distributions invariably ship with SSH (the OpenSSH implementation, to be precise), but you can download it from its Web site, http://www.openssh.com, if necessary.