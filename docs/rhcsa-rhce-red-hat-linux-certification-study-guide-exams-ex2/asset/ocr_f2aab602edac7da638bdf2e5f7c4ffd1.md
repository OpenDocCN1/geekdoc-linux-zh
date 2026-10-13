> Exam Watch
> The virt-install command is one method to address the RHCSA objective “Install Red Hat Enterprise Linux systems as virtual guests.”

For many, that’s simpler than configuring the GUI Virtual Machine Manager. The Creating Domain message at the end of Figure 2-14 starts a VNC window with a graphical view of the given installation program.

If you make a mistake with the virt-install command, you can abort the process by pressing CTRL-C. But be aware that newly created VM is still running. And there’s now a configuration

file and virtual disk for that VM. If you try to rerun the virt-install command with the same name for the VM, an error message will appear. Thus, if you want to use the same name for the VM, take the following steps:

+   1. Stop the VM just created. If it’s the tester1.example.com system shown in Figure 2-14, you can do so with the following command:
+      # virsh destroy tester1.example.com
+   2. Delete the associated XML configuration file in the /etc/libvirt/qemu directory. For the given system name, that file would be tester1.example.com.xml.
+   3. If desired, you may also want to delete the virtual disk file, normally created in the /var/lib/libvirt/images directory. However, this is not necessary if the file is of an acceptable size, as it is reusable. For the given system name, that file would be tester1.example.img.
+   4. With the following command, restart the VM daemon, to erase the tester1.example.com system from RAM:
+      # /etc/init.d/libvirtd restart
+   5. Now you’ll be able to run the virt-install command again with the same name for the VM.

```
# virsh destroy tester1.example.com
```

```
# /etc/init.d/libvirtd restart
```

# The virt-install Command and Kickstart

For Kickstart installations described later in this chapter, the virt-install --prompt command can’t be used to cite a Kickstart configuration file. For that purpose, you’ll need to understand some of the key switches associated with the virt-install command, as shown in Table 2-3.

For example, the following virt-install command would install a system named outsider1.example.org automatically from a Kickstart file named ks1.cfg from the