# INSIDE THE EXAM

# Manage Virtual Machines

The RHCSA objectives suggest that you need to know how to

+   - Access a virtual machine's console
+   - Start and stop virtual machines
+   - Configure systems to launch virtual machines at boot
+   - Install Red Hat Enterprise Linux systems as virtual guests

It's reasonably safe to assume the VMs in question are based on Red Hat's default VM solution, KVM. While in Chapter 1, you installed that solution during the installation process on a 64-bit system, you may also need to install the associated packages on a live system during an exam. In addition, there is a Virtual Machine Manager graphical console used by Red Hat to manage such VMs. Of course, that Virtual Machine Manager is a front end to command line tools that can also be used to install a system. Such tools can also be used to configure that system to be started automatically during the boot process.

While the Red Hat exam blog noted in Chapter 1 suggests that you'll take an exam on a "pre-installed" system, that doesn't preclude installations on VMs. So in this chapter, you'll learn how to set up an installation of RHEL 6 on KVM.

# Kickstart Installations

The RHCSA objectives state that you need to know how to

+   - Install Red Hat Enterprise Linux automatically using Kickstart

To that end, every RHEL installation includes a sample Kickstart file, based on the given installation. In this chapter, you'll learn how to use that file to automate the installation process. It's a bit trickier than it sounds, as the sample Kickstart file must be modified first, beyond unique settings for different systems. But once configured, you'll be able to set up as many installations of RHEL as you need using that baseline Kickstart file.

# Access Remote Systems

The RHCSA objectives state that you need to know how to

+   - Access remote systems using SSH and VNC

If systems administrators had to be in physical contact with every system they have to administer, half of their lives would be spent en route from system to system. With tools such as the Secure Shell (SSH) and Virtual Network Computing (VNC), administrators have the ability to do their work remotely. While this chapter focuses on the uses of SSH, Chapter 9 focuses on the configuration of VNC. While SSH is automatically installed in a standard configuration in RHEL 6, custom configuration options such as passphrases are the province of the RHCE exam.