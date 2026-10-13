# INSIDE THE EXAM

# A Virtual Host

The RHCSA assumes that you know how to “configure a physical machine to host virtual guests.” In other words, you need to be able to prepare a system to house VMs where other instances of RHEL (or even other operating systems such as Microsoft Windows) can be installed.

As this is RHEL, this is based on the Red Hat default VM system, KVM. As appropriate rebuild distributions such as CentOS and Scientific Linux use the same source code, they also use KVM. In this chapter, not only will you install RHEL, but also you will install those packages that support KVM.

# Default File Sharing Configuration Services

RHCSAs are expected to know how to “Configure a system to run a default configuration HTTP server” and “Configure a system to run a default configuration FTP server.” The default Red Hat solutions for these services are the Apache Web server and the very secure FTP (vsFTP) server. While these services can be complex, the steps required to set up these

servers to share files are fairly simple. In fact, no changes are required to the default configuration files for these services. Some of the related steps described in this chapter depend on skills presented in future chapters.

The original release of the RHCSA was worded slightly differently: “Deploy file sharing services with HTTP/FTP.” I believe this provides a significant clue to Red Hat’s intent with these objectives. To that end, you’ll examine how to set up these services as file servers, based on their default configurations.

# Using Other Versions of Red Hat

For the purpose of this chapter, you can install RHEL 6 using a paid subscription or from a demonstration DVD. You can also use one of the rebuild distributions. However, while RHEL 6 is based in part on the work done on the Fedora Linux distribution, it’s based in part on both the Fedora 12 and 13 releases. So it’s possible if you use Fedora 12 or 13, the configuration files may in some cases be quite different from RHEL 6. Later versions of Fedora are likely to have features not found in RHEL 6.