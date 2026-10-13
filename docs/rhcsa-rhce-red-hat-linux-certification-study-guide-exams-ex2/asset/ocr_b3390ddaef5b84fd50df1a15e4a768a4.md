# CERTIFICATION OBJECTIVE 7.01

# The Red Hat Package Manager

One of the major duties of a system administrator is software management. New applications are installed. Services are updated. Kernels are patched. Without the right tools, it can be difficult to figure out what software is on a system, what is the latest update, and what applications depend on other software. Worse, you may install a new software package only to find it has overwritten a crucial file from a currently installed package.

The Red Hat Package Manager (RPM) was designed to alleviate these problems. With RPM, software is managed in discrete packages. An RPM package includes the software with instructions for adding, removing, and upgrading those files. When properly used, the RPM system can back up key configuration files before proceeding with upgrades and removals. It can also help you identify the currently installed version of any RPM-based application.

RPMs and the rpm command are far from ideal, which is why it has been supplemented with the yum command. With a connection to a repository such as that available from the RHN or third-party "rebuilds" such as Scientific Linux, you'll be able to use yum to satisfy dependencies.

# What Is a Package?

In the generic sense, an RPM package is a container of files. It includes the group of files associated with a specific program or application, which normally includes binary installation scripts as well as configuration and documentation files. It also includes instructions on how and where these files should be installed and uninstalled.

An RPM package name usually includes the version, the release, and the architecture for which it was built. For example, the fictional penguin-3.4.5-26.x86_64.rpm package is version 3.4.5, build 26, and the x86_64 indicates that it is suitable for computers built to the AMD/Intel 64-bit architecture.

*Many RPM packages are CPU-specific. You can identify the CPU type for the system with the uname -i or uname -p commands. More information is available from the contents of the /proc/cpuinfo file.*

![](bbox=[0.05, 0.9, 0.18, 0.98])