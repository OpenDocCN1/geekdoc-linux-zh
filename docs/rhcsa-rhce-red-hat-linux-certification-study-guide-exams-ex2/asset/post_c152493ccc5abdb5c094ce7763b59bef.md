
That's just seven packages! Of course, in most configurations, they'll pull in other packages as dependencies. But that's all you really need to configure VMs on a physical RHEL 6 system with a 64-bit CPU. While none of these packages are in the Virtualization Tools group, those packages may be helpful in real life. It includes tools that can help read and manage the VM disk images. If you choose to convert images from Xen or from some formats of VMware, the virt-v2v package is what you need.

Installation with the Add/Remove Software tool is fairly simple. Just select (or deselect) desired packages and click Apply. If there are dependent packages that also require installation, you'll be prompted with the full list of those packages. Of course, from the command line interface, you can install these packages with the `yum install packagename` command.

## The Right KVM Modules

In most cases, installation of the right packages is good enough. Appropriate modules should be loaded automatically. Before KVM can work, the associated modules must be loaded. Run the following command:

```bash
# lsmod | grep kvm
```

If KVM modules are properly loaded, you'll see one of the following two sets of modules:

```bash
kvm_intel  45578  4
kvm       291875  1 kvm_intel
```

or

```bash
kvm_amd    35678  4
kvm       261575  1 kvm_amd
```

As the module names suggest, the output depends on the CPU manufacturer. If you don't get this output, first make sure the hardware is suitable. And as suggested in Chapter 1, make sure the `svm` or `vmx` flag is listed in the contents of the `/proc/cpuinfo` file. Otherwise, additional configuration may be required in the system BIOS or UEFI menu. Some menus include specific options for hardware virtualization, which should be enabled.

If one of the noted flags exists in the `/proc/cpuinfo` file, the next step is to try loading the applicable modules. The simplest method is with the `modprobe` command. The following command should also load the dependent module, whether it be `kvm_intel` or `kvm_amd`:

```bash
# modprobe kvm
```

## Configure the Virtual Machine Manager

The Virtual Machine Manager is part of the `virt-manager` package. And you can start it in a GUI with the command of the same name. Alternatively in the GNOME desktop, click **Applications | System Tools | Virtual Machine Manager**. It opens the Virtual Machine Manager window shown in Figure 2-2.

In some cases, two hypervisors, also known as virtual machine monitors, are shown on the localhost system. These hypervisors work with QEMU as processor emulators within the virtual machines. QEMU is also known by its former acronym, the quick emulator. If a usermode emulator appears, it is appropriate if you want to run 32-bit applications on a 64-bit system. But that's inefficient. In most cases, you'll want to create and manage VMs in the localhost (QEMU) regular mode.

![](img/9139201cfcaf4292284a0eed074928e5_73_0.png)

> As of the RHEL 6 release, the QEMU usermode emulator is subject to bug 634876 at https://bugzilla.redhat.com. The issue was addressed with an update to the virt-manager package.

**FIGURE 2-2**
Virtual Machine Manager

![](img/9139201cfcaf4292284a0eed074928e5_73_1.png)

## Connections to Hypervisors

If desired, the KVM-based VMs can be configured and administered remotely. All you need to do is connect to the remote hypervisor. To do so, click **File | Add Connection**. It opens an Add Connection window that allows you to select:

- A hypervisor, normally KVM or Xen. (Xen was the default hypervisor on RHEL 5.)
- A connection, which may be local, or remote using a connection such as SSH.

Remote connections can be given with the hostname or IP address of the remote system.

## Configuration by Hypervisor

Each hypervisor can be configured in some detail. Right-click the localhost (QEMU) hypervisor and select **Details** in the pop-up menu that appears. It opens a details window named after the host of the local system, as shown in Figure 2-3.

As shown, the Overview tab lists the basics of the VM configuration, as discussed in Table 2-2.

**FIGURE 2-3**
VM Host Details.

![](img/9139201cfcaf4292284a0eed074928e5_74_0.png)

**TABLE 2-2 VM Host Details**

| Setting | Description |
|---|---|
| Connection | Universal Resource Identifier (URI) for the hypervisor |
| Hostname | Hostname for the VM host |
| Hypervisor | QEMU is used by KVM |
| Memory | Available RAM from the physical system for VMs |
| Logical CPUs | Available CPU cores; "4" indicates four CPUs or a quad-core system |
| Architecture | CPU architecture |
| Autoconnect | Whether to automatically connect to the hypervisor during the boot process |

For the next section, stay in the host details window for the current hypervisor.

## Virtual Networks on a Hypervisor

Now you'll examine the networks configured for VMs within the Virtual Machine Manager. In the host details window for the current hypervisor, click the **Virtual Networks** tab. The default virtual network shown in Figure 2-4 illustrates the standard network for VMs created with this hypervisor.

**FIGURE 2-4**
VM Host Details.

![](img/9139201cfcaf4292284a0eed074928e5_75_0.png)

You'll note the given network is configured to start automatically when the VM is booted. So if there's an appropriate virtual network card configured on the VM, along with a client command associated with the Dynamic Host Configuration Protocol (DHCP), it's automatically given an IP address from the noted range. As noted in the figure, assigned addresses are configured to forward information using Network Address Translation (NAT).

With the buttons in the lower-left part of the screen, you can add a new virtual network, start and stop an existing virtual network, and delete that network. In Exercise 2-1, you'll create a second virtual network. For the next section, stay in the host details window for the current hypervisor.

## EXERCISE 2-1: Create a Second Virtual Network

In this exercise, you'll create a second virtual network on the standard KVM hypervisor in the GUI Virtual Machine Manager. This exercise requires a RHEL 6 system configured, is based on an in-process installation of RHEL 6, and assumes the Virtual Machine Manager as discussed earlier in this chapter.

1. Right-click the standard localhost (QEMU) hypervisor. In the pop-up menu that appears, select **Details**.
2. In the Host Details window that appears with the name of the local system, select the **Virtual Networks** tab.
3. Click the plus sign in the lower-left corner of the Virtual Networks tab to open the Create A New Virtual Network Wizard.
4. Read the instructions, which you will follow in coming steps. Click **Forward** to continue.
5. Assign a name for the new virtual network. For the purpose of this book, enter the name `outsider`. Click **Forward** to continue.
6. If not already input, type in the `192.168.100.0/24` network address in the Network text box. The system automatically calculates appropriate entries for other network information, as shown in the illustration. Click **Forward** to continue.

## on the Job

![](img/9139201cfcaf4292284a0eed074928e5_77_0.png)

Take care to avoid IP address conflicts with existing hardware on the local network, such as with routers and wireless access points. For example, at least one cable “modem” uses IP address `192.168.100.1` for maintenance. In that case, the noted `192.168.100.0/24` network would make that cable “modem” inaccessible. If you have such hardware, do change the network address shown in the illustration.

7. Now you can select the range of IP addresses within the configured network that can be assigned by a DHCP client. Per Chapter 1, Table 1-2, you'll configure a static IP address for the `outsider1.example.org` system on this network. As long as the noted `192.168.100.100` IP address is outside the range of DHCP-assignable IP addresses, no changes are required. Make any needed changes and click **Forward** to continue.
8. Now you'll want a system that forwards network communication to the physical network, if only because that's how systems on this network communicate with systems on different virtual networks, possibly on different virtual hosts. The destination can be Any Physical Device, in NAT mode, to help hide these systems from remote hosts. Unless you want to limit routing from VMs to a specific physical network card, the defaults under Forwarding To Physical
