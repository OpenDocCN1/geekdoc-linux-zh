Updating and patching the desktop client is done using up2date. The RHN alert notification tool is used to alert the user that an update or patch is available. The update process can also be automated.

Using RHN, there are three types of modules:

+   - Update
- Management
- Provisioning

These modules determine the service level you get from RHN.

The Update module only gives basic update capabilities such as:

+   - Access to a Web interface to manage the systems.
- Priority e-mail notification of new updates and errata.
- Errata information provides a list of all available errata updates for each system.
- RPM dependency checks makes sure that every applied update gets all necessary dependencies.
- Auto update allows a system to download and install errata updates automatically.

The Management module provides all capabilities of the Update module plus extended management capabilities.

+   - Systems can be managed as a group.
- System permissions can be assigned to administrators and groups of systems.
- Actions such as updates can be scheduled for a system or group.
- System search allows for searching systems and groups by package, errata, or system specifications.
- Detailed comparisons of packages can be produced between systems or against a pre-built package profile.

The Provisioning module is really useful when RHN is used to create new clients. Along with everything in the Update and Management module, Provisioning also provides:

+   - Bare metal provisioning - A tool to automatically provision a system using kickstart to deploy operating system, packages, and activation keys.
- Existing state provisioning - Provision system to take the state of a predefined installation.
- A rollback functionality to roll back updates.