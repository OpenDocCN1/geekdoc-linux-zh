
Loaded plugins: langpacks, product-id, subscription-manager
rhel-7-workstation-rpms/x86_64 | 3.4 kB 00:00:00
No packages needed for security; 0 packages available

Note that the above command runs in a non-interactive mode, so it can be used in scripts for automated checking whether there are any updates available. The command returns an exit value of 100 when there are any security updates available and 0 when there are not. On encountering an error, it returns 1.

Analogously, use the following command to only install security-related updates:

```
[~]# yum update --security
```

Use the **updateinfo** subcommand to display or act upon information provided by repositories about available updates. The **updateinfo** subcommand itself accepts a number of commands, some of which pertain to security-related uses. See Table 3.1, “Security-related commands usable with yum updateinfo” for an overview of these commands.

## Table 3.1. Security-related commands usable with yum updateinfo

| Command | Description |
| :--- | :--- |
| `advisory [advisories]` | Displays information about one or more advisories. Replace *advisories* with an advisory number or numbers. |
| `cves` | Displays the subset of information that pertains to CVE (*Common Vulnerabilities and Exposures*). |
| `security` or `sec` | Displays all security-related information. |
| `severity [severity_level ]` or `sev [severity_level]` | Displays information about security-relevant packages of the supplied *severity_level*. |

## 3.1.2. Updating and Installing Packages

When updating software on a system, it is important to download the update from a trusted source. An attacker can easily rebuild a package with the same version number as the one that is supposed to fix the problem but with a different security exploit and release it on the Internet. If this happens, using security measures, such as verifying files against the original RPM, does not detect the exploit. Thus, it is very important to only download RPMs from trusted sources, such as from Red Hat, and to check the package signatures to verify their integrity.

See the **Yum** chapter of the Red Hat Enterprise Linux 7 System Administrator's Guide for detailed information on how to use the **Yum** package manager.

### 3.1.2.1. Verifying Signed Packages

All Red Hat Enterprise Linux packages are signed with the Red Hat GPG key. GPG stands for **GNU Privacy Guard**, or **GnuPG**, a free software package used for ensuring the authenticity of distributed files. If the verification of a package signature fails, the package may be altered and therefore cannot be trusted.

The **Yum package manager** allows for an automatic verification of all packages it installs or upgrades. This feature is enabled by default. To configure this option on your system, make sure the `gpgcheck` configuration directive is set to **1** in the `/etc/yum.conf` configuration file.

Use the following command to manually verify package files on your filesystem:

```
rpmkeys --checksig package_file.rpm
```

See the Product Signing (GPG Keys) article on the Red Hat Customer Portal for additional information about Red Hat package-signing practices.

### 3.1.2.2. Installing Signed Packages

To install verified packages (see Section 3.1.2.1, “Verifying Signed Packages” for information on how to verify packages) from your filesystem, use the `yum install` command as the **root** user as follows:

```
yum install package_file.rpm
```

Use a shell glob to install several packages at once. For example, the following commands installs all `.rpm` packages in the current directory:

```
yum install *.rpm
```

> **IMPORTANT**
> 
> Before installing any security errata, be sure to read any special instructions contained in the erratum report and execute them accordingly. See Section 3.1.3, “Applying Changes Introduced by Installed Updates” for general instructions about applying changes made by errata updates.

## 3.1.3. Applying Changes Introduced by Installed Updates

After downloading and installing security errata and updates, it is important to halt the usage of the old software and begin using the new software. How this is done depends on the type of software that has been updated. The following list itemizes the general categories of software and provides instructions for using updated versions after a package upgrade.

> **NOTE**
> 
> In general, rebooting the system is the surest way to ensure that the latest version of a software package is used; however, this option is not always required, nor is it always available to the system administrator.

### Applications

User-space applications are any programs that can be initiated by the user. Typically, such applications are used only when the user, a script, or an automated task utility launch them.

Once such a user-space application is updated, halt any instances of the application on the system, and launch the program again to use the updated version.

### Kernel

The kernel is the core software component for the Red Hat Enterprise Linux 7 operating system. It manages access to memory, the processor, and peripherals, and it schedules all tasks.

Because of its central role, the kernel cannot be restarted without also rebooting the computer. Therefore, an updated version of the kernel cannot be used until the system is rebooted.

#### KVM

When the qemu-kvm and libvirt packages are updated, it is necessary to stop all guest virtual machines, reload relevant virtualization modules (or reboot the host system), and restart the virtual machines.

Use the `lsmod` command to determine which modules from the following are loaded: `kvm`, `kvm-intel`, or `kvm-amd`. Then use the `modprobe -r` command to remove and subsequently the `modprobe -a` command to reload the affected modules. For example:

```
~]# lsmod | grep kvm
kvm_intel                143031  0
kvm                      460181  1 kvm_intel
~]# modprobe -r kvm-intel
~]# modprobe -r kvm
~]# modprobe -a kvm kvm-intel
```

#### Shared Libraries

Shared libraries are units of code, such as glibc, that are used by a number of applications and services. Applications utilizing a shared library typically load the shared code when the application is initialized, so any applications using an updated library must be halted and relaunched.

To determine which running applications link against a particular library, use the `lsof` command:

```
lsof library
```

For example, to determine which running applications link against the `libwrap.so.0` library, type:

```
~]# lsof /lib64/libwrap.so.0
COMMAND     PID USER   FD   TYPE DEVICE SIZE/OFF   NODE NAME
pulseaudi 12363 test mem  REG  253,0    42520 34121785
/usr/lib64/libwrap.so.0.7.6
gnome-set 12365 test mem  REG  253,0    42520 34121785
/usr/lib64/libwrap.so.0.7.6
gnome-she 12454 test mem  REG  253,0    42520 34121785
/usr/lib64/libwrap.so.0.7.6
```

This command returns a list of all the running programs that use TCP wrappers for host-access control. Therefore, any program listed must be halted and relaunched when the tcp_wrappers package is updated.

#### systemd Services

systemd services are persistent server programs usually launched during the boot process. Examples of systemd services include sshd or vsftpd.

Because these programs usually persist in memory as long as a machine is running, each updated systemd service must be halted and relaunched after its package is upgraded. This can be done as the root user using the systemctl command:

```
systemctl restart service_name
```

Replace *service_name* with the name of the service you want to restart, such as sshd.

### Other Software

Follow the instructions outlined by the resources linked below to correctly update the following applications.

- Red Hat Directory Server – See the Release Notes for the version of the Red Hat Directory Server in question at https://access.redhat.com/site/documentation/en-US/Red_Hat_Directory_Server/.
- Red Hat Enterprise Virtualization Manager – See the Installation Guide for the version of the Red Hat Enterprise Virtualization in question at https://access.redhat.com/site/documentation/en-US/Red_Hat_Enterprise_Virtualization/.

## 3.2. USING THE RED HAT CUSTOMER PORTAL

The Red Hat Customer Portal at https://access.redhat.com/ is the main customer-oriented resource for official information related to Red Hat products. You can use it to find documentation, manage your subscriptions, download products and updates, open support cases, and learn about security updates.

### 3.2.1. Viewing Security Advisories on the Customer Portal

To view security advisories (errata) relevant to the systems for which you have active subscriptions, log into the Customer Portal at https://access.redhat.com/ and click on the Download Products & Updates button on the main page. When you enter the Software & Download Center page, continue by clicking on the Errata button to see a list of advisories pertinent to your registered systems.

To browse a list of all security updates for all active Red Hat products, go to Security → Security Updates → Active Products using the navigation menu at the top of the page.

Click on the erratum code in the left part of the table to display more detailed information about the individual advisories. The next page contains not only a description of the given erratum, including its causes, consequences, and required fixes, but also a list of all packages that the particular erratum updates along with instructions on how to apply the updates. The page also includes links to relevant references, such as related CVE.

### 3.2.2. Navigating CVE Customer Portal Pages

The CVE (Common Vulnerabilities and Exposures) project, maintained by The MITRE Corporation, is a list of standardized names for vulnerabilities and security exposures. To browse a list of CVE that pertain to Red Hat products on the Customer Portal, log into your account at https://access.redhat.com/ and navigate to Security → Resources → CVE Database using the navigation menu at the top of the page.

Click on the CVE code in the left part of the table to display more detailed information about the individual vulnerabilities. The next page contains not only a description of the given CVE but also a list of affected Red Hat products along with links to relevant Red Hat errata.

### 3.2.3. Understanding Issue Severity Classification
