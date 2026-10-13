# Table 36.3: Workstation actions for the vmware-cmd utility.

| Option* | Description |
|---|---|
| Getconnectedusers | List users connected to the VM and their IP address |
| getstate | Gets the execution state of the VM |
| start <powerop_mode> | Powers on or resumes a VM |
| stop <powerop_mode> | Stops a VM |
| reset <powerop_mode> | Resets a VM |
| suspend <powerop_mode> | Suspends a VM |
| setconfig <variable> <value> | Sets a configuration variable |
| getconfig <variable> | Retrieves the value for a configuration variable |
| setguestinfo <variable> <value> | Sets a guest info variable |
| getguestinfo <variable> | Retrieves the value for a guest info variable |
| getid | Retrieves the VM ID |
| getpid | Retrieves the process ID of the running VM |
| getproductinfo <prodinfo> | Gets various product information |
| connectdevice <device_name> | Connects a virtual device to a VM |
| disconnectdevice <device_name> | Disconnects a virtual device from a VM |
| getconfigfile | Retrieves the path to the configuration file |
| getheartbeat | Retrieves the heartbeat value of the guest OS |
| getuptime | Retrieves the uptime of the guest OS |
| getremoteconnections | Retrieves the number of remote connections to a VM |
| gettoolslastactive | Retrieves the number of seconds since last notification from the tools |
| getresource <variable> | Retrieves a VM resource |
| setresource <variable> <value> | Sets a VM resource |
| setrunasuser <username> <password> | Sets the user that the VM runs as |
| getrunasuser | Retrieves the user that the VM runs as |
| getcapabilities | Retrieves the access permissions of the current user on a VM |
| addredo <disk_device_name> | Adds a redo log to a virtual disk |
| commit <disk_device_name> <level> <freeze> <wait> | Commits the redo log of a virtual disk |
| answer | Answers a question for a VM requesting input |

*Workstation options must always include the full path to the virtual machine's configuration file.