12. The next screen relates to local or specialized storage devices. If you have one or more “regular” local hard drives (SATA, PATA, or a virtual hard drive on a KVM system), select Basic Storage Devices, and click Next.

13. If there are new hard disks being applied to the system, you’ll be asked to confirm changes to those disks.

14. If there’s a previous version of RHEL (or a similar recognized Linux operating system) installed, you may see a Fresh Installation option. If it appears, select it. Otherwise, Anaconda skips to the next step.

15. You’re now asked to give a hostname for the local system, such as server1.example.com. Click Configure Network to open the Network Connections tool described in Chapter 4. In some cases, the network settings configured in Step 6 may not be reflected in this tool. Make appropriate changes and click Next to continue.

16. Now you’ll see a world map, where you can select the time zone of the local system. The System Clock Uses UTC option is a reference to the local hardware clock and the atomic realization of Greenwich Mean Time. (UTC is a non-English language acronym also based on a political compromise.) While incompatible with Microsoft Windows, the UTC option supports changes for daylight saving time. Make appropriate changes and click Next to continue.

17. The next step is to enter the password for the root administrative user, twice. Do so and click Next to continue.

18. The next step, shown in Figure 1-6, determines how space on configured hard disks, local and remote, is used. The options are fairly well explained in the figure. To summarize:

+   - **Use All Space** Removes all partitions on all configured devices, including those created by non-Linux operating systems.
+   - **Replace Existing Linux System(s)** Removes all Linux-formatted partitions, including those created for other Linux distributions such as Fedora and Ubuntu Linux.
+   - **Shrink Current System** Takes account of unused space on available existing partitions, shrinks those partitions, allowing that free space to be used for the new installation.
+   - **Use Free Space** Uses existing free space for the new installation.
+   - **Create Custom Layout** Supports custom configuration using Disk Druid, the Red Hat disk partitioning tool, during the installation process.