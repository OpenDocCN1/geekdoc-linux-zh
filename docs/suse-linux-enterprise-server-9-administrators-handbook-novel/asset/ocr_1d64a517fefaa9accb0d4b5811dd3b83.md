# NOTE

Realistically, a system should be hardened right after it has been installed and still in a clean state. This is not possible in most cases, and you will probably think of hardening the system after it shows signs of being compromised. If this is the case, you should at least check and replace all suspected system utilities (such as ls and ps) and add-on applications (such as Apache) with known good copies before starting on the hardening process.

This chapter presents you with ideas and theories associated with overall system security from both a hardware and software point of view, starting with an overview of the principles behind system hardening.

# System Hardening Principles

The principles of system hardening can be summarized with a single maxim: “Unless explicitly permitted, access is strictly forbidden.” In other words, the access to any system service or resource should default to none, unless you specifically allow it. This way, you know what you are opening up and why. It is much more difficult to work the other way around because there is always the slight chance that someone important was missed and later turns out to be a costly oversight. So, the general idea is to install only those packages that the system actually needs and open only those firewall ports that are required by these services. That way, potential intruders can’t exploit software that isn’t present or running on the system. However, removing a package isn’t always possible (due to dependencies) or practical. Therefore, at the very least, unneeded services should be disabled.

The following general tasks are associated with securing the operating system and its services:

+   - Disable or remove all unneeded services. For services that are required, ensure you are running the latest version.
+   - Use the secure version of a service daemon wherever and whenever possible. For instance, use vsftpd for FTP services instead of one that doesn’t support SSL.
+   - Disable or remove all unused user accounts.
+   - Keep up-to-date with software updates, for both the operating system and applications, at least in regard to security patches. For SLES servers, you can easily keep them updated using the YaST Online Update (YOU) feature. (Refer to Chapter 2, “Updating the Server,” for more details.)