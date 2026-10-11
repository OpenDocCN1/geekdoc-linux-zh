# **Mandatory Access Control**

In contrast to Discretionary Access Control, where the user determines the permissions granted to the object she creates, Mandatory Access Control permissions are set by the administrator according to a policy.

The following is described:

+   - SELinux
+   - AppArmor

# **SELinux**

Mandatory access control in SELinux is possible in two ways: *Type Enforcement (TE)* and *Role Based Access Control (RBAC)*. To learn more about these, we recommend the web site of the National Security Agency at <http://www.nsa.gov/selinux/>. The NSA initiated the SELinux project.

The main configuration files for SELinux on an RHEL system are stored in the directory `/etc/selinux/`.

SELinux is normally activated by the init process at the boot time. Activation during boot can be disabled by entering the boot parameter `selinux=0` or by setting the SELINUX parameter in `/etc/selinux/config` to `disabled`.

There are two types of SELinux policies: *targeted* (only targeted network daemons are protected) and *strict* (full SELinux protection). Only one type of policy can be active in the Kernel at a time. Which policy is used when activating SELinux is defined by the parameter **SELINUXTYPE** in the file `/etc/selinux/config`.

Policies are created using the m4 macro language. The sources are kept in `/etc/selinux/<POLICY-NAME>/src/policy/`, while the binaries can be found in `/etc/selinux/<POLICY-NAME>/policy/`.