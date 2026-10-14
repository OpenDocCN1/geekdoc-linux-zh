# # An Overview of LILO

The Linux boot loader is usually installed in the MBR (details below, on the following page, and in Section *Installing and Uninstalling LILO* on page 103). When started, LILO already has access to both real mode hard disks and, due to its installation, is able to find all of the data it needs from the two hard drives without requiring any partitioning data. Because of this, operating systems can be booted from the first as well as from the second hard disk. The entries in the partition table that standard DOS MBR uses to mark the active partition are ignored when using LILO in the MBR.

An important difference from the standard DOS boot sequence is that you can select any of the installed systems at boot time when using LILO. After loading the MBR into memory, LILO is started and you are asked to select one of the installed operating systems.

# ## About LILO

LILO is a versatile boot manager. It loads boot sectors of partitions from which to boot an operating system or it loads the Linux kernel and boots Linux. Furthermore, LILO provides the important option of passing a command to the kernel. For security reasons, this can be protected totally or partially with a password.

# ## Booting with LILO

When LILO is launched, it displays the text LILO and a greeting message (entered during installation — see Section *Other LILO Configuration Options* on page 99). Thereafter, a command prompt appears:

```
```text
boot:
```
```

Here, select your operating system by entering its name. It is then booted. The name of the operating system was set during installation. At this point, you can pass a parameter line to the Linux kernel. Get a list of all the operating system names available by pressing `Tab`.

# ## The Components of LILO

The LILO machinery consists of the following components:

+   - the beginning, or *first stage*, of the LILO code in a boot sector that activates the system boot.