You can stop inet from running at system bootup, by selecting Off, don't start inet. You can use the default configuration, by selecting On with default configuration. Or, you can configure inet yourself by selecting On, with custom configuration...

We will guide you through editing the inet configuration to allow you to add or remove services from your server.

![](bbox=[0.27, 0.191, 0.834, 0.506])

Figure 117. YaST2: Editing the inet configuration

You have four options to add a new configuration to the server:

+   - **Create** - This allows you to add a new service to the server.
- **Delete** - This will delete the selected service from the system.
- **Edit** - This allows you to edit the currently selected service.
- **Activate/Deactivate** - This will stop the service, but will not delete the entry. This has the same effect as deleting entry, but will not remove it from the configuration file. If it activates the service, it will take it out of the deactivated state and allow it to run.

114 Linux System Administration and Backup for IBM @serverX and Netfinity