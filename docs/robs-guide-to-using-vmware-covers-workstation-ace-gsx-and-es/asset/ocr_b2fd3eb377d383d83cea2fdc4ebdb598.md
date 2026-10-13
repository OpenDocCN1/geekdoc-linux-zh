# 6.2 Running Virtual Machines from the Command Line

You can start virtual machines from the command line in several ways. One of them is by using the VMware executable itself. There are also two separate executables that you can use: vmrun and vmware-fullscreen.exe (for Windows). All three options are explained in this chapter.

# Parameters for the VMware executable

It can be very useful to start virtual machines when your host starts. You can do this by adding commands to a startup script or you could start virtual machines from scripts, or trigger them from other applications in your host system.

The syntax for starting VMware Workstation from the command line is:

```
vmware [OPTIONS] [\<path_to_config>\<config>.vmx]
```

Table 6.1: Listing of command line switches for VMware executable.

| Command Line Switch | Description |
|---|---|
| -x | Automatically powers the virtual machine on when VMware starts. |
| -X | Automatically powers the virtual machine on when VMware starts and switches to full screen mode. |
| -q | Closes the virtual machine's tab when the machine powers off, and also exits VMware Workstation if no other virtual machines are running at the same instance as vmware.exe. |
| -s NAME=VALUE | Sets the specified variable to the specified value. Any variable names and values that are valid in the configuration file may be specified on the command line with the -s switch. |
| -p parentDisk childDisk | Points disks to the correct parent disk |
| -m (Linux host only) | Starts the program in quick switch mode on a Linux host. |
| -k KVM_FILE | Specifies a list of virtual machines. |
| -v | Displays the product name, version and build number of VMware Workstation. |
| \<path_to_config>\<config>.vmx | Do not forget to use quotes around file names that have spaces in them; otherwise parts of the path will be seen as separate parameters. |