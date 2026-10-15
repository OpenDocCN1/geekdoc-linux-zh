+   - How to install Solaris as a guest on a LINUX or Windows host
+   - To cover the commands and primitives (Solaris-only commands in parentheses)
+     `dladm (Solaris), ipadm(Solaris), ifconfig, jail, pkg, pkgadd(Solaris), VBoxManage, VirtualBox, iocage, xz , zoneadm(Solaris), zonecfg(Solaris), zonename(Solaris)`

# 25.1 INTRODUCTION TO VIRTUALIZATION METHODOLOGIES AND BACKGROUND

Computer hardware virtualization is the simulation, to various degrees, of hardware platforms, parts of them, or only the functionality required to run one or more operating systems (OSs). It abstracts and thus hides the physical characteristics of the hardware from the users. Traditionally, the software that controlled virtualized machines was known as the hypervisor. Currently, the hypervisor is often called a virtual machine monitor (VMM). For example, in VirtualBox, the virtual machine (VM) VirtualBox manager is the graphical front-end for a VMM.

Platform virtualization is accomplished on any given hardware by host software (the hypervisor), which creates a simulated computer environment, a VM, for its guest software. The guest software can be as small as a single user application or as large as complete OSs. The guest software executes as if it were running directly on the physical hardware.

Virtualization comes with some performance disadvantages, both in resources required to run the hypervisor and in reduced performance on the VM guest compared with running applications on a nonvirtualized host physical machine.

A VM can be more easily controlled and inspected from outside than a physical one, and its configuration is more flexible. This is very useful in kernel development and for teaching OS courses. A new VM can be implemented as needed without the need for an up-front hardware purchase.

A VM can easily be moved from one physical machine to another as needed. An unrecoverable fault inside a VM guest does not harm the host system, so there is no risk of crashing the host OS.

Examples of virtualization implementations:

+   1. Running one or more applications that are not supported by the host OS: A VM running the required guest OS could allow the desired applications to be run, without altering the host OS.
+   2. Evaluating an alternate OS: The new OS could be run within a VM, without altering the host OS.
+   3. Server virtualization: Multiple virtual servers in containers could be run on a single physical server, to utilize more fully the hardware resources of the physical server.
+   4. Duplicating specific environments: A VM could, depending on the virtualization software used, be duplicated and installed on multiple hosts, or restored to a previously backed-up system state.