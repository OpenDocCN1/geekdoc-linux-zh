| Area | Description |
|---|---|
| CPU | The type of CPU and the amount of processing load |
| Memory | The amount of memory installed on the system and its usage pattern |
| Hard disk, CD-ROM, and floppy drives | The disk capacities and their usage status |
| Network cards | The network devices which are operational and their usage statistics |
| Mouse | The kind of mouse being used by the system |
| Keyboard | The kind of keyboard being used by the system |
| Display | The display card detected by the system and its current usage status. |
| Various PCI and USB devices | The various devices detected by the system |
| Sound | The sound card detected and used by the system |

Much of the information can be found using special files that are maintained dynamically by the operating system. These files can be found by looking in the /proc directory. The files are special because they are generated "on demand" by the operating system, and do not actually exist on the file system except when requested (for example, by the ls /proc command).

You can view the contents of these files by using the cat command (which prints to the screen the contents of any file whose name is passed as a parameter to it, as we'll see in the next few examples). Alternatively, you could use a text editor such as gedit.

# CPU-related Information

The CPU information detected by the operating system can be found by displaying the contents of the file /proc/cpuinfo. This is shown below: