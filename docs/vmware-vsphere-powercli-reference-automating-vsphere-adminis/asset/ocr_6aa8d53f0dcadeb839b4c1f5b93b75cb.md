reating virtual machines (VMs) can be a large part of any virtualization administrator's job. With the perceived ease of deployment, virtualization administrators are often asked to meet deployment schedules that aren't possible in the physical world. To meet these demands, they have to use the full toolkit at their disposal. When it comes to deploying virtual machines, the tools provided are templates and customization specifications. Their use is a key part of any administrator's game. In this chapter, you will learn how to create templates and customization specifications, deploy guests, and maintain templates over the long term.

# # Use Customization Specifications

A customization specification is a collection of information used to customize a guest operating system. This task can be done in conjunction or independently on an existing VM as long as the machine in question has the following items installed:

+   - VMware Tools
- 32-bit or 64-bit hardware corresponding to the 32-bit or 64-bit operating system to be installed
- SCSI disks attached at SCSI node 0:0

Guest customization is accomplished through the use of finalization scripts that are executed through the GuestOperationsManager core API. Although this technique works wonderfully, it requires that the finalization script be written for the guest operating system. As of vSphere 4.1, guest customization is supported on all versions of Windows since 2003, as well as most modern RedHat, Debian, Ubuntu, and most Linux distributions. Most Linux distributions based on an officially supported kernel will work as well.

> A list of the supported operating systems is available online at the vSphere compatibility matrix at http://pubs.vmware.com/vphere-60/index.jsp@com.vmware.vphere.vm_admin.doc/GUID-E63B6FAA-8D35-428D-B40C-744769845906.html.