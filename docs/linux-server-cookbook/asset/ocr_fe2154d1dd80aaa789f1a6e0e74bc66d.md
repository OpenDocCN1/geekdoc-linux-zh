+   • subversion: Deploys a subversion repository.

+   • systemd: Manage systemd units.

+   • sysvinit: Manage SysV services.

+   • tempfile: Creates temporary files and directories.

+   • template: Template a file out to a target host.

+   • unarchive: Unpacks an archive after (optionally) copying it from the  
+   local machine.

+   • uri: Interacts with Web services.

+   • user: Manage user accounts.

+   • validate_argument_spec: Validate role argument specs.

+   • wait_for: Waits for a condition before continuing.

+   • wait_for_connection: Waits until the remote system is  
+   reachable/usable.

+   • yum: Manages packages with the yum package manager.

+   • yum_repository: Add or remove YUM repositories.

# # Roles

*Roles* organize *Tasks*, *Variables*, *Handlers*, *Templates*, and static files in a  
directory. This structure can be reused in different projects. The directory  
containing *Roles* is, by default, called *roles*. Inside, there is a folder with the  
name of the role. The *Role* directory structure is as follows:

```
roles/role_name/
├── defaults
│   └── main.yml
├── files
├── handlers
│   └── main.yml
├── meta
│   └── main.yml
├── README.md
└── tasks
```