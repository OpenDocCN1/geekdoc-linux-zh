# SELF TEST ANSWERS

# Configure KVM for Red Hat

+   1. Three kernel modules are associated with KVM: kvm, kvm_intel, and kvm_amd.
+   2. The tool that can configure KVM-based VMs in the GUI is the Virtual Machine Manager.

# Configure a Virtual Machine on KVM

+   3. The command that starts the Virtual Machine Manager in the GUI is virt-manager. Since menus are not always available, the Applications | System Tools | Virtual Machine Manager click sequence is not an acceptable answer.
+   4. The directory with default virtual disks for the Virtual Machine Manager is /var/lib/libvirt/images.
+   5. The command that can be used to create a new VM is virt-install.

# Automated Installation Options

+   6. The command that starts the GUI-based Kickstart configuration tool is system-config-kickstart.
+   7. The name of the Kickstart file in the /root directory that documents how RHEL was installed is anaconda-ks.cfg.
+   8. The directive in the Kickstart configuration file related to networking is network.
+   9. The directive that points to the given FTP installation server is url --url ftp://server1.example.com/pub/inst.
+   10. The directive in the Kickstart configuration that would shut down a system after installation is complete is shutdown.

# Administration with the Secure Shell

+   11. The ssh command switch that is used to specify a different user for remote logins is -l.
+   12. The ssh command switch that enables access to remote GUI utilities is -X. The -Y switch is also an acceptable answer.