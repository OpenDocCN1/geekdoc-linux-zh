screen. To use this command, simply enter **lsmod** at the shell prompt, as shown in the example here:

| Module | Size | Used by |
| :--- | :--- | :--- |
| lp | 10913 | 0 |
| parport_pc | 37547 | 1 |
| af_packet | 23229 | 0 |
| joydev | 11942 | 0 |
| st | 41564 | 0 |
| fuse | 75897 | 3 |
| ... | | |

To view more information about a particular loaded module, you can use the **modinfo** command. You can first use lsmod to find the name of the module in question and then enter **modinfo module_name** at the shell prompt. In the preceding example, one of the modules displayed by lsmod is **joydev**. This is your system’s joystick kernel module. To view more information about this particular module, you can enter **modinfo joydev** at the shell prompt, as shown in the example here:

```
```
ws1:~ # modinfo joydev
filename:	/lib/modules/2.6.34.7-0.7-desktop/kernel/drivers/input/joydev.ko
license:	GPL
description:	Joystick device interfaces
author:	Vojtech Pavlik vojtech@ucw.cz
serverversion:	B57DA6AAE9B8102A01E91
alias:	input:b*tv*p*e-*e*1,*k*r*C0,*r*t*a*m*1*g*f*w*
alias:	input:b*tv*p*e-*e*1,*k*r*130,*r*t*a*m*1*g*f*w*
alias:	input:b*tv*p*e-*e*1,*k*r*120,*r*t*a*m*1*g*f*w*
alias:	input:b*tv*p*e-*e*3,*k*r*r*a*6,*m*1*g*f*w*
alias:	input:b*tv*p*e-*e*3,*k*r*r*a*8,*m*1*g*f*w*
alias:	input:b*tv*p*e-*e*3,*k*r*r*a*0,*m*1*g*f*w*
depends:
vermagic:	2.6.34.7-0.7-desktop SMP preempt mod_unload modversions
```
```

To load a kernel module, you first need to run the **depmod** command from the shell prompt. This command is used to build a file named **modules.dep** that is stored in **/lib/modules/kernel_version/**, as shown here:

```
```
ws1:/lib/modules/2.6.34.7-0.7-desktop # ls
kernel			modules.builtin.bin	modules.order		systemtap
modules.alias	modules.dep		modules.soortdep	vdsoc
modules.alias.binmodules.dep.bin	modules.symbols	weak-updates
modules.builtin	modules.devname	modules.symbols.bin
```
```

Within this file, **depmod** lists the dependencies between modules. This helps other kernel module management utilities ensure that dependent modules are loaded whenever you load a module.

With the **modules.dep** file created, you can now go ahead and load kernel modules. You can use one of two different commands to do this. The first is the **insmod** command. The syntax for **insmod** is **insmod module_filename**. The module filename is usually a kernel module located in a subdirectory of **/lib/modules/kernel_version/kernel/**. For example, if you wanted to load the driver for a standard PC parallel port, you would enter **insmod /lib/modules/version/kernel/drivers/parport/parport_pc.ko** at the shell prompt.