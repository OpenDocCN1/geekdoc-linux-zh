![](bbox=[0.05, 0.12, 0.55, 0.45])

Figure 7.9 Just like a new physical hard drive, a new virtual drive needs to be partitioned with fdisks before it can hold an operating system.

8. If your virtual disk is larger than 512MB (and it should be!), you see a question about enabling large disk support. You should answer Y to enable large disk support so you can format the virtual disk as a single large partition. The only reason to answer N is if you plan to dual boot the virtual machine with an old version of DOS or Windows 3.1 or an early revision of Windows NT. Save yourself a lot of hassle and don’t.

9. When the fdisks main menu appears, select option 1, Create DOS Partition.

10. When the Create DOS Partition menu appears, select option 1, Create Primary DOS Partition.

11. fdisks briefly scans the virtual disk and then asks whether you want to use the maximum available size (see Figure 7.10). Answer Yes.

12. fdisks accesses the drive to create the partition and then prompts you to press Esc to exit fdisks, as shown in Figure 7.11. Do so.

13. After exiting fdisks, you need to reboot the virtual machine for the new partition to be recognized. The easiest way is to click the Reset button on the VMware window. You can also try sending Ctrl+Alt+Del through the keyboard or through the VMware Power toolbar menu.

14. Let the virtual machine reboot. (Leave the Windows 95 setup floppy in the drive!)

15. If the startup disk asked you about CD-ROM options before, you are asked again. Start the virtual machine with the same options you used the first time.

16. You still need to format the new partition you created. At the A:\> prompt, type format C: /s.