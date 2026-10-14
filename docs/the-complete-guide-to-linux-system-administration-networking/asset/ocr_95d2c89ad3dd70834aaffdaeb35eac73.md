11. Looking again on the left side of the qconf window, click on **Network File Systems** below the File Systems item.

12. With Network File Systems selected, look at the right side of the window and locate SMB file system support (to mount Windows shares, etc.). Click the checkbox next to that item so that it contains a check.

13. On the left side, below the Network File Systems item, click **Native Language Support.**

14. On the right side of the window, scroll down the list to see what character sets the Linux kernel supports. By default, most are created as kernel modules. Select one of them near the top of the list that includes the label "Codepage" with a number. Write down the code page number of that item.

15. On the left side of the window, click **Cryptographic options**, near the bottom of the list.

16. None of the cryptographic options are compiled into the kernel by default, but the kernel can support many different methods of encrypting network traffic. Review the options listed.

17. Choose File, then Quit on the menu of the qconf window.

18. When prompted, click **Save Changes** to create a new configuration file based on the selections you have made.

19. The kernel configuration you created is stored in the file .config in the /usr/src/linux-2.6.5-1.358 directory. Open that file in a text editor with this command:

`vi .config`

20. Search for the text CONFIG_NLS_CODEPAGE to find the list of native language support options. In vi, type / then type the search text and press Enter. When you find that part of the file, locate the line matching the code page that you selected in Step 16.

21. Explore the .config file as you wish, then exit the text editor.

22. If you have sufficient time and your instructor's permission, compile a new kernel based on your configuration by entering this command while in the /usr/src/linux-2.6.5-1.358 directory:

`make dep; make bzImage; make modules`

You see hundreds of lines scroll by as the kernel is compiled. Remember that the new kernel file is being created, but that this does not affect the kernel that you are running (including the next time you restart). The finished kernel is stored as a file called bzImage in the directory /usr/src/linux-2.6.5-1.358/arch/i386/boot.