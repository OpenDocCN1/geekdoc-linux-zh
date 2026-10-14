
of OS (suite) it will install. Here’s the first segment of the command that we will build off of (but don’t hit Enter just yet):

```
$ sudo vmbuilder kvm ubuntu
```

There are different options you can choose from based on which hypervisor and suite you choose, and you can pass the --help argument after each one to get a list of specific options:

```
$ sudo vmbuilder kvm ubuntu --help
```

The vmbuilder script will create a directory in your current directory and dump the VM’s disk there, so if you have set aside a special place on the disk to store VM files, be sure to change to that directory first. Here’s a sample relatively basic vmbuilder command that will create an Ubuntu Lucid VM called test1:

```
$ sudo vmbuilder kvm ubuntu --suite lucid --flavour virtual --arch i386 --hostname test1 --libvirt qemu:///system --rootsize=2048 --swap size=256 --user ubuntu --pass insecure -d test1-kvm
2010-04-17 12:17:04,193 INFO : Calling hook: preflight_check
2010-04-17 12:17:04,196 INFO : Calling hook: set_defaults
2010-04-17 12:17:04,197 INFO : Calling hook: bootstrap
...
2009-02-27 16:52:31,480 INFO    Cleaning up
```

After I run the command, the script will go out and retrieve all of the packages and files it needs and automatically build the VM for me. Below I describe each of the options I chose:

- **--suite lucid**
  The --suite option chooses which Ubuntu version to install. I chose lucid here but you could also choose dapper, feisty, gutsy, hardy, intrepid, jaunty, or karmic

- **--flavour virtual**
  There are different kernel flavors available for Ubuntu. The virtual flavor chooses the JeOS kernel that’s optimized for VMs, but there are

a number of different kernels from which you can choose, depending on which Ubuntu suite and architecture you choose.

- **--arch i386**  
  This is the processor architecture to use for my VM. If I don’t specify this, it will default to the host architecture. Valid options are `i386`, `amd64`, and `lpia`.

- **--hostname test1**  
  If you don’t specify a hostname, the VM will default to a hostname of ubuntu. This is fine until you decide you want to create more than one VM, at which point you will get an error that the domain ubuntu already exists. Use the `--hostname` option, so that not only can you specify the hostname within the OS, you can also specify the unique name that will be registered with KVM.

- **--libvirt qemu:///system**  
  The `--libvirt` option will automatically add this VM to my local KVM instance.

- **--rootsize 2048 and --swapsize 256**  
  For basic VMs you probably just want a single disk with a root and swap partition. In that case you can use `--rootsize` and `--swapsize` to specify the root and swap partition sizes in megabytes. There is also an `--optsize` option that will set up a separate /opt partition.

- **--user ubuntu and --pass insecure**  
  You will want some sort of default user on the system so once it is built you can log in to it, unless your network uses LDAP or some other network authentication. The `--user` and `--pass` arguments let me specify the default user and password to use; otherwise both will default to ubuntu. You can also use the `--name` option to set the full name of the user.

- **-d test1-kvm**  
  By default, `vm-builder` will install the VM’s root disk under the ubuntu-kvm directory in the user’s home directory. Of course, once you set up one VM, you won’t be able to reuse the same directory, so the `-d` option lets you specify the location of the destination directory.

Once the install completes, I will see that a new test1-kvm directory was created in my current directory and inside is the disk file for that VM:

```bash
$ ls test1-kvm/
run.sh tmpHHSJGZ.qcow2
```

In addition, my new VM will be registered with KVM, and its XML file, which defines its settings, will be installed under /etc/libvirt/qemu/test1.xml and look something like this:

```xml
<domain type='kvm'>
  <name>test1</name>
  <uuid>907a0091-e31f-ef2b-6181-dc2d1225ed65</uuid>
  <memory>131072</memory>
  <currentMemory>131072</currentMemory>
  <vcpu>1</vcpu>
  <os>
    <type arch='i686' machine='pc-0.12'>hvm</type>
    <boot dev='hd'/>
  </os>
  <features>
    <acpi/>
  </features>
  <clock offset='utc'/>
  <on_poweroff>destroy</on_poweroff>
  <on_reboot>restart</on_reboot>
  <on_crash>destroy</on_crash>
  <devices>
    <emulator>/usr/bin/kvm</emulator>
    <disk type='file' device='disk'>
      <source file='/home/ubuntu/vms/test1-kvm/tmpHHSJGZ.qcow2'/>
      <target dev='hda' bus='ide'/>
    </disk>
    <interface type='network'>
      <mac address='52:54:00:c6:18:b7'/>
      <source network='default'/>
      <model type='virtio'/>
    </interface>
    <input type='mouse' bus='ps2'/>
    <graphics type='vnc' port='-1' autoport='yes' listen='127.0.0.1'/>
    <video>
      <model type='cirrus' vram='9216' heads='1'/>
    </video>
  </devices>
</domain>
```
