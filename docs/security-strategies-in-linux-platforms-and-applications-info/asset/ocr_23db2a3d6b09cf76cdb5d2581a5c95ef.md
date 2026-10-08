# PART 3 | Building a Layered Linux Security Strategy

| TABLE 14-3 Commands to include in a forensic toolkit |
| COMMAND | DESCRIPTION |
| cat | The cat command is available from the coreutils package. For more information, see http://www.gnu.org/software/coreutils/ |
| date | The date command is available from the coreutils package. |
| dd | The dd command is available from the coreutils package. |
| dmesg | The dmesg command is available from the util-linux-ng package, which can be downloaded from the Linux kernel servers at http://ftp.kernel.org/pubinux/lutils/util-linux-ng/ |
| nc | While the nc command is available from a variety of sources, option is coupled with the nmap command, available online from http://nmap.org/download.html. |

The steps required to install packages are similar to those described for the Sleuth Kit. Detailed instructions should be available in a file named INSTALL in the directory of unpacked source code. Some customization may be required for example: it's helpful to configure the source code to redirect tools to a specific directory with a command similar to the following:

```
# /.configure --prefix=/tools
```

Once the given tools are written to a CD or DVD, you'll be able to mount media on suspect systems, secure in the knowledge that the commands written to such media will not be changed.

# Forensic Live Media

Many groups have created their live media for forensic data recovery. While very few of these options support recovery of volatile data such as files in the /proc/ directory, most of these options provide excellent support for the investigator who wants to create a copy of suspect hard drives and analyze the data on those drives in detail. Several options for forensic live media are listed in Table 14-4. Some of these options include commands for recovering volatile data from a Microsoft operating system. Most of these options can boot into a customized version of Linux, loaded in RAM, with tools that can diagnose and otherwise examine files associated with a Linux or Microsoft system on a local device. In general, drive is not mounted when the live CD or DVD is loaded. This list does not include the live CD/DVD distributions that include additional forensic tools. In fact, most live CD/DVD distributions include command-line tools that can help with forensic analysis. But be careful. Standard live CD/DVD distributions may use or otherwise overwrite information on a swap partition. When booting forensic

![](bbox=[0.198, 0.945, 0.225, 0.975])