
(1 for itself and 1 because it can claim the quorum disk). The same situation holds true for member2. So if both members could come up with enough votes to reach quorum, we have a problem. Fortunately, the CNX is ready for this type of scenario, and as a result one member will panic, probably with one of the last two panic strings listed above. The member that has claimed the quorum disk will continue to function.

## 17.5 The Boot Sequence

To see how a cluster is formed (or for that matter how a node becomes a member), let’s see what happens when you boot a node in a cluster.

When the “boot” command is issued from the console of a node that’s part of a cluster configuration that node will boot off of its member boot disk. Contained on the boot disk at logical block number (LBN) zero is the boot block.

```
CPU 0 booting

(boot dk7b100.1.0.3.2 -flags A)
block 0 of dk7b100.1.0.3.2 is a valid boot block
```

### 17.5.1 From the Boot Block to the Kernel

![](img/a0df85c2e542a8d6c913113908553aa4_494_1.png)

The boot block code points to the primary bootstrap code at LBN 64.

```
reading 19 blocks from dkb100.1,0,3,2
bootstrap code read in
Building RAM table
base = 20000, image_start = 0, image_bytes = 2600
initializing HWBP at 2000
initializing page table at 1f2000
initializing machine state
setting affinity to the primary CPU
jumping to bootstrap code
```

The primary bootstrap code loads the osf_boot program, located on the boot_partition (partition “a”) of the boot disk. It is the osf_boot program that handles prompting for the kernel and subsystem attributes in an interactive boot (i.e., boot -fl i). The osf_boot program is also responsible for loading the kernel.

```
UNIX boot - Wednesday August 01, 2001

Loading vmunix ...
Loading at 0xfffffe0000023000

Sizes:
text = 8624320
data = 1778320
bss = 3900872
Starting at 0xfffffe0000242360
```

Once the kernel is loaded and starts to execute, many things happen prior to single-user mode including cluster formation! So, please turn your hymnals to “The Ballad of V. M. Unix” and follow along. Please feel free to shout out or sing along if the muse strikes you.

### 17.5.2 Loading the Kernel to Subsystem Configuration

![](img/a0df85c2e542a8d6c913113908553aa4_495_0.png)

While we don’t intend to walk through every step in the kernel boot sequence, we want to point out a few steps to help in understanding how a cluster is formed.

One of the kernel’s earliest tasks is to read the sysconfigtab file. This is the reason why the sysconfigtab file is located in the etc directory on the boot_partition. Once the sysconfigtab file is read, the kernel loads the attributes into the configuration management database (cfgdb), loads the Configuration Manager (cm) subsystem, and sets up the subsystem callback mechanism. After the callback mechanism is loaded, the kernel configures all the static kernel subsystems.

If you are curious about how the kernel knows which subsystems to configure, take a look at the conf.c file in any member's /sys/HOSTNAME directory.

```
# cd /usr/sys/MOLARI ; grep -p static_subsys_list conf.c \
> | grep CFG_STATE_LOADED | cut -d, -f2 | cut -d" -f2 | tee /tmp/conf_c
rm
rmvm
rdg
clubase
kevm_clu
drd
cnx
kch
dim
mcs
clua
lcs_nl
lcs_ll_tcp
lcs_ll_mct
cfs
cms
token
icsnet
clsm
...
```

The conf.c file is created by the config(8) program which is run by the doconfig(8) script.

Of course, once a system is up and running it is usually much more straightforward to query the configuration manager using the sysconfig program to see which subsystems are statically loaded.

```
# sysconfig -m | grep static | cut -d: -f1 | tee /tmp/sysconfig
```

Using the diff(1) command on the two files we created in the previous two examples, we can see that there are no differences.

```
# diff /tmp/conf_c /tmp/sysconfig
<no output>
```

There are approximately 97 static subsystems loaded into the kernel. Of course this number can vary depending on your configuration and the options chosen.

```
# wc -l /tmp/sysconfig /tmp/conf_c
     97 /tmp/sysconfig
     97 /tmp/conf_c
    194 total
```
