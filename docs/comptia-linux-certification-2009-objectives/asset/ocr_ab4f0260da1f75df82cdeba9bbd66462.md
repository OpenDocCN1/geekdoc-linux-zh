# # ACTIVITY 11-5

# ## Configuring SELinux

**Before You Begin:**
On *srvA*, you have logged in as root in the CLI.

**Scenario:**
Your system contains confidential information that needs to be protected from any unauthorized access. You need to enable access control to prevent processes from reading or tampering data and programs, bypassing application security mechanisms, executing unauthorized programs, or interfering with other processes in violation of the system security policy.

| What You Do | How You Do It |
| :--- | :--- |
| **1.** Configure the SELinux mode. | a. Enter `vi /etc/sysconfig/selinux` to configure the SELinux settings.<br>b. Enter `SELINUX=disabled` to go to the SELinux mode configuration line.<br>c. Press **I** to switch to the insert mode.<br>d. Set `SELINUX=permissive` to configure access control. |
| **2.** Check the SELinux policy settings. | a. Verify that the security policy is set to `SELINUXTYPE=targeted`.<br>b. Press **Esc** to switch to the command mode.<br>c. Save and close the file.<br>d. Enter `reboot` to apply the settings. |