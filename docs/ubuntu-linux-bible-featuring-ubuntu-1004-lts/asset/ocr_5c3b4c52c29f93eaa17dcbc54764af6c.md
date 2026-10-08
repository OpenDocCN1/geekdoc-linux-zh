# Part II: Ubuntu for Desktop Users

and similar settings on your new Ubuntu system by converting data into formats that are used by equivalent Ubuntu applications and then copying the converted data to your Ubuntu system.

This chapter focuses on migrating your data from a Microsoft Windows system to an Ubuntu Linux system. The same general concepts and tasks often apply if you are migrating from a Mac OS system-tem, but although most of the examples in this chapter relate to dif-ferent flavors of Windows, I will also provide tips that highlight Macintosh migration tasks without providing step-by-step instructions.

# Overview of Migration Scenarios

Chapters 2, "Installing Ubuntu," and 3, "Installing Ubuntu on Special-Purpose Systems," dis-ussed how to install Ubuntu, with a focus on installation on a new machine or on an existing machine where you can dedicate specific partitions to Ubuntu so you can dual-boot. When migrating from a Windows system, you obviously need to be able to access the data from your Windows system. When you get to that information differs based on the type of Ubuntu installa-tion that you're:

+   * Installing Ubuntu on a new machine and leaving Windows on: This is the easiest migration scenario because you can copy file data from your Windows system via a network connection or by copying your Windows data to a USB thumb drive. You can do any necessary file conversions on the Windows sys-tem, leaving your original data intact, and then copy the converted data to your Ubuntu system to verify it.

+   * Dual-booting an existing machine: Still an easy scenario, you can mount your Windows partition(s) on your Ubuntu system and copy file data to Ubuntu. You may have to boot into Windows in order to convert some of your files, but you can copy the converted files directly from your Windows filesystem once you are running Ubuntu.

+   * Converting a single system: This is the trickiest scenario—you must use a backup of your Windows data as the location from which you can copy files. You must also do all necessary file conversions on the Windows system before you do the backup, or the Linux system after you are running Ubuntu.

Both of the last two scenarios require making changes to your existing Windows system, so it is critical to do a complete backup of your Windows system before installing Ubuntu. See the next section for details.

This chapter discusses various ways of migrating your existing Windows data to an Ubuntu sys-tem. Frankly, I hope that you will never need to read some of the sections of this chapter, but they're here if you need them. I suggest the following sequence of events in order to smoothly migrate your data to your Ubuntu system:

+   1. Start Outlook or Outlook Express and export your Address Book information in a generic format such as a CSV file. You may not need this, but it's always handy to have a spare copy of this information in an application-independent format such as a CSV file.

320