| BUTTON OR ACTION | DESCRIPTION |
|---|---|
| START LAB | Start all virtual machines in the classroom. |
| SHUTDOWN LAB | Stop all virtual machines in the classroom. |
| OPEN CONSOLE | Open a new tab in the browser and connect to the console of the virtual machine. Students can log in directly to the virtual machine and run commands. In most cases, students should log in to the virtual machine and use ssh to connect to the other virtual machines. |
| ACTION → Start | Start (power) on the virtual machine. |
| ACTION → Shutdown | Gracefully shut down the virtual machine, preserving the contents of its disk. |
| ACTION → Power Off | Forcefully shut down the virtual machine, preserving the contents of its disk. This is equivalent to removing the power from a physical machine. |
| ACTION → Reset | Forcefully shut down the virtual machine and reset the disk to its initial state. **Caution: Any work generated on the disk is lost.** |

At the start of an exercise, if instructed to reset a single virtual machine node, click ACTION → Reset for only the specific virtual machine.

At the start of an exercise, if instructed to reset all virtual machines, click ACTION → Reset

If you want to return to the classroom environment to its original state at the start of the course, you can click DELETE LAB to remove the entire classroom environment. After the lab has been deleted, you can click PROVISION LAB to provision a new set of classroom systems.

> WARNING The DELETE LAB operation cannot be undone. Any work you have completed in the classroom environment up to that point will be lost.

# # The Autostop Timer

The Red Hat Online Learning entitles students to a certain amount of computer time. To help conserve allotted time, the ROL classroom has an associated countdown timer, which shuts down the classroom environment when the timer expires.

To adjust the timer, click MODIFY to display the New Autostop Time dialog box. Set the number of hours until the classroom should automatically stop. Click ADJUST TIME to apply this change to the timer settings.