and install VMware Tools. It is not necessary to install VMware Tools under Linux; see the next section. Under Windows, wait to install VMware Tools until after you have installed the full operating system as explained in the next section.

# VMware Tools

VMware Tools is software that resides on the VM and improves its performance, functionality, and the ease with which it can be managed. For example, VMware Tools can improve graphics and mouse performance. It enables the VM and host to share folders, drag and drop, synchronize time, as well as copy and paste.

The Linux **open-vm-tools** package holds an open-source implementation of VMware Tools. Because VMware has merged the functionality of VMware Tools into the kernel and **open-vm-tools**, you do not need to install VMware Tools on a Linux system when **open-vm-tools** is installed.

With the guest operating system installed on the VM, select *from the VMware menu Player: Manage->Install VMware Tools*. Alternatively, the VMware Player window might display a button labeled *Install Tools*; clicking this button performs the same function as making the menu selection. If you are prompted to download VMware Tools, do so.

Once the software is downloaded and ready to install, Windows asks whether you want to allow VMware to make changes to the computer; click *Yes*. You might need to supply the *root password for the VM* in order to install VMware Tools. Also, you might need to unmount the virtual DVD from the virtual DVD drive before you can install VMware Tools. If you are prompted with *Disconnect anyway and override the lock?* click *Yes*. When the Software Updates window displays *All updates finished*, click *Close*. VMware Tools is installed.

# Cloud Computing

Cloud computing is the result of evolution and the combination of virtualization, networking, and powerful hardware. Cloud computing allows users to reap the benefits of these tools without knowing how to use each individually, needing only a lightweight system to access the cloud.

As an alternative to setting up the hardware and software to run a cloud, you can purchase a cloud computing platform as a service. Buying the service means the provider takes care of the infrastructure, software, and management (including scaling), and it is faster to set up and (frequently) cheaper to build than setting up and running your own cloud server.

OpenShift (www.openshift.com) is a cloud computing platform as a service from Red Hat. The open-source software that runs the service is named OpenShift Origin. OpenShift maintains the service and scales as needed.