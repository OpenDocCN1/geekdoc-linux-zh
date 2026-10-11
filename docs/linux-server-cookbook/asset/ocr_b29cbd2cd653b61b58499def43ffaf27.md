| | |
| :--- | :--- |
| remove | Removes the specified package(s). |
| search | Searches for a specific package(s). |
| upgrade | Upgrades the system or the package(s) indicated to the latest version available. |

*Table 4.19: Actions for the commands dnf and yum*

Some of the popular global options are shown in *table 4.20*:

| **Option** | **Description** |
| :--- | :--- |
| `--downloadonly` | Download package(s) and dependencies only without performing the installation. |
| `--show-duplicates` | If software repositories offer multiple versions for the same package, all of them will be listed. Default *dnf/yum* shows only the latest version. |
| `-v`, `--verbose` | Shows debug information. |
| `-y`, `--assumeyes` | Does not ask the users if they want to confirm the operation. |

*Table 4.20: Popular global options for the commands dnf and yum*

In the following figures, the different tasks performed using command **dnf** are shown:

+   * *Figure 4.30* checks if there is any available package update available:

![](bbox=[0.19, 0.49, 0.86, 0.58])

*Figure 4.30: Output example checking the packages that can be updated.*

+   * Upgrade the Linux distribution to the latest version available.
+       * *Figure 4.31* shows that the first part of the output is the transaction summary information:

![](bbox=[0.22, 0.68, 0.9, 0.9])