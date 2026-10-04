+   - The system must have at least 300MB of available disk space; 1GB is recommended.
- The programmable read-only memory (PROM) must be level 1.1 or later.

# System Configurations

Before installing the OS, you'll need to determine the system configuration to be installed. System configurations, or types, are defined by the way they access the root (/), the /usr file systems, and the swap area. The five system configurations are server, standalone, diskless client, dataless client, and AutoClient.

# Server

A server system has the following file systems installed locally:

+   - The root (/) and /usr file systems, plus swap space
- The /export, /export/swap, and /export/home file systems, which support client systems and provide home directories for users
- The /opt directory or file system for storing application software

Servers can also contain the following software to support other systems:

+   - OS services for diskless clients and AutoClient systems
- Solaris CD image and boot software for networked systems to perform remote installations
- JumpStart directory for networked systems to perform custom JumpStart installations

# Standalone

On a standalone system, the OS is loaded on a local disk and the system is set to run independent of other systems for portions of the OS. It might be networked to other standalone systems. A networked standalone system can share information with other systems on the network, but it can function autonomously because it has its own hard disk with enough space to contain the root (/), /usr, and /home file systems and swap space. The standalone system has local access to operating system software, executables, virtual memory space, and user-created files.

# Diskless Client

A diskless client is a system with no local disk that is dependent on a server for all of its software and storage area. The OS is located on a server on the network. The diskless client