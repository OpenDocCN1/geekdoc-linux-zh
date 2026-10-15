# Tip

You should use the -1 option whenever you back up the root (/) filesystem. If you don't use this option, you also back up /proc, which wastes a lot of space on your tape because /proc is a virtual filesystem that contains some very large pseudo-files. What's more, on restoration, you might cause problems when you write to the pseudo-files in /proc, causing system settings to change.

# Note

Some floppy-based tape devices require that you format a tape prior to use. Others, including most SCSI- and EIDE-based drives, have no such requirement, since tapes are sold pre-formatted. The ftape documentation describes how to format a tape.

Although tar is capable of backing up a computer or even an entire network, it has limits, such as the danger involved in creating compressed backups with the program. Therefore, many people prefer to use programs such as cpio and afio, or commercial packages such as BRU. I present backup principles with tar in the rest of this chapter because tar is commonly available and because it's the basis for the smbtar program described later in the chapter. The basic principles are the same for other programs, so if you prefer to use another program, you should have few or no problems adapting the information here to your software of choice.

In addition to separate packages, assorted programs function as GUI front ends to tar or some other tape backup program. Figure 13.1, for instance, shows the KDat program, which comes with the popular KDE GUI environment. KDat serves as a front end to tar, allowing you to create and manipulate backup sets.

# Note

Although GUI backup software can be convenient and is often less intimidating than command-line utilities, it has two major drawbacks. First, in the case of a complete system recovery, you usually must learn how to use the GUI software's command-line equivalents, and doing so in a disaster-recovery situation is more stressful and difficult than doing so when your system is fully functional. Second, for network backup, you should probably automate the backup process. Although some GUI tools provide schedulers in the GUI environment, one of the best ways to automate backups is to create cron jobs to run the backup from scripts, as described later in this chapter, in the section "Creating cron Jobs to Back Up Regularly." Scripted backups call for command-line tools rather than GUI tools.