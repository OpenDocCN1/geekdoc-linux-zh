These are located in **/etc/rc.config.d.** (These files do not exist on some systems.)

# Link Files

These files are used to control the order in which scripts execute. These are actually links to execution scripts to be executed when moving from one run level to another. These files are located in the directory for the appropriate run level, such as **/sbin/rc0.d** for run level 0, **/sbin/rc1.d** for run level 1, and so on. The files in this directory that begin with an "S" are startup scripts, and those that end in a "K" are shutdown scripts. (These links are found in **/etc** instead of **/sbin** on some systems.)

# Sequencer Script

This script invokes execution scripts based on run-level transition. This script is usually **/sbin/rc**.

Figure 12-1 shows a commonly used directory structure for startup and shutdown scripts.