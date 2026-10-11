To unmask a service:

```
sudo systemctl unmask [service_name]
```

Masking is more extreme than disabling and should be used with caution.

# Running Background Processes

In Linux systems, background processes, also known as daemons, are programs that run continuously in the background, providing various services to the system or users. Understanding how to manage these processes is crucial for system administrators and power users.

# Types of Background Processes

+   1. **System Daemons**: These are background processes that start during system boot and run continuously until the system is shut down. Examples include `sshd` (SSH server), `crond` (cron daemon), and `systemd` itself.
+   2. **User Daemons**: These are background processes started by individual users, often for specific tasks or applications.
+   3. **Detached Processes**: Regular processes that are manually "detached" from the terminal and sent to the background.

# Starting a Process in the Background

To start a process in the background from the command line, you can use the `&` symbol at the end of the command: