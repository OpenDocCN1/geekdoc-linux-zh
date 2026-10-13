information on repository management, see Linux Patch Management, written by this author, published by Prentice Hall.

# CERTIFICATION OBJECTIVE 7.04

# More Package Management Tools

Whether a system is connected to the RHN or remote repositories provided by a distribution like CentOS or Scientific Linux, it uses the same basic package management tools. Each of these alternatives uses the rpm command to process RPM packages. They use the yum command to satisfy dependencies and install groups of packages. And that makes sense, as the rebuild distributions are built on the same source code as RHEL 6.

Those similarities extend to GUI-based package management tools. While the identity of these tools have changed between RHEL 5 and RHEL 6, they're still front ends to the rpm and yum commands. They take advantage of the package groups configured in the .xml file described in Chapter 2. Since Red Hat uses GNOME as the default GUI desktop environment, the associated tools for RHEL 6 are based on that interface.

However, one thing that the rebuild distributions don't have is access to the RHN. That situation may only be temporary, Red Hat has recently started to release RHN software under open-source licenses. And developer groups are at work with projects like Spacewalk. That's important for the enterprise, as the RHN provides tools to administer groups of systems remotely from a single Web-based interface.

![](bbox=[0.1, 0.75, 0.18, 0.85])

> Subscriptions to the RHN includes access to the actual RHEL 6 operating system releases. Trial subscriptions support RHN access for that trial period. However, if you or your organization can't afford RHN subscriptions for every system, consider the tools provided by the Spacewalk project. It provides all of the functionality of the RHN, except for timely access to updates.

For RHEL 6, GUI-based package management tools are based on the PackageKit. However, it's quite possible that the PackageKit won't be available on a server, or perhaps even a system configured for a Red Hat exam. If you absolutely need the PackageKit, install the required RPMs with the yum install gnome-packagekit