# 3 STEP-BY-STEP INSTALLATION

| Attributes | Value |
| :--- | :--- |
| Updated: | 3 minutes ago | Self-tests: | Completed OK |
| Powered On: | 72.5 days | Power Cycles: | 956 |
| Temperature: | 24° C / 75° F | Bad Sectors: | None |
| Self-Assessment: | Passed | Overall Assessment: Disk is healthy |
| Refresh | Run Self-test |
| Read SMART Data, making up the disk | Test the disk for errors |
| ID | Attribute | Assessment Value |
| 1 | Read Error Rate | Normalized: 100 Worst: 100 Threshold, while reading data from the disk. A non-zero value indicates a problem with either the disk or the media | Value: 45178 |
| 2 | Throughput Performance | Average efficiency at the disk | Normalized: 100 Worst: 100 Threshold: 80 |
| 3 | Spunup Time | Time needed to spin up the disk | Normalized: 100 Worst: 100 Threshold: 75 Value: 2 | |
| 4 | Start/Stop Count | Don't warn if the disk is failing | Normalized: 99 Worst: 99 |

Figure 3-16 SMART data as displayed by palimpsest this window you can run various self-tests and scroll through the information at the bottom of the window.

# ubiquity: Setting UP PARTITIONS

While you are installing Ubuntu,iquity offers two ways to partition a disk: guided and manual. Guided partitioning sets up partitions—one for swap space (page 37) and one for /root, where the entire Ubuntu files systems mounted; page 37), The amount of space occupied by root depends on which guided option you select. Manual partitioning enables you to set up partitions of any type and size; you can also specify the mount point for each partition.

# ADVANCED GUIDED PARTITIONING

“Prepare Disk Space” on page 66 explained how to use guided partitioning to partition an empty disk. This section explains how guided partitioning works on a disk that is already partitioned.

Depending on the contents of the hard disk you are installing Ubuntu on, theiquity partition editor presents different choices. Figure 3-17 shows the Prepare disk space for a hard disk with one partition that occupies the entire disk. That partition holds a Windows system. This screen shows all possible choices. In some cases, not all of these choices appear. Click the radio button adjacent to a choice to select it. The choices possible are outlined here:

+   * Install them by side, choosing between each startup—Allows you to shrink a partition and use the space free by this operation to install Ubuntu. You can use this choice to set up a dual-boot system