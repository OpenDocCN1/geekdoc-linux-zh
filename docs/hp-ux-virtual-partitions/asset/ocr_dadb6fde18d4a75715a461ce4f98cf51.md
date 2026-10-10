drive is *tapessys*. We'll read the tape to a directory on *orl* using **dd** and **cpio** (see the earlier **cpio** section for an explanation of the options) in the following example:

```
# hostname
orl
# pwd
/tmp/remotecpiofiles
# remsh tapessys "dd if=/dev/rmt/0m bs=8k" | cpio -icvBdum
.
envd.action2
envd.action5
swagent.log
ntp
OBAMHBAo01020
aaaa01558
.
.
.
.

aaaa01487
OBAMFEAa01630
cmd_res8215
tmp_cfg_file
cmd_res8708
OBAMHBAb07762
exclude.temp
arch.include.1
3580 blocks
0+358 records in
0+358 records out
#
```

This command runs a remote shell (**remsh**) to run the **dd** command on *tapessys*. The output of this command is piped to **cpio** on our local system to extract the archive. In this example, only the *if* option was used to specify the input file. The *of* option, which specifies the output file was not needed. If you were to perform a **dd** of a disk device to a tape drive, the *of* would be the tape drive on your system, such as */dev/rmt/0m*.