![](bbox=[0.178, 0.068, 0.882, 0.353])

Figure 5.2 A NASM-IDE error message box.

exited NASM-IDE with that file still in a window, NASM-IDE will load that file from disk and put it in a window, just as it was when you last shut down NASM-IDE. If, on the other hand, you’re bringing up NASM-IDE for the very first time, or if there was no file in a window when you last shut NASM-IDE down, there will be no file in a window when the NASM-IDE environment appears. NASM-IDE remembers what it was doing when you last shut down, and absent other instructions, it will pick up precisely where it left off.

NASM-IDE’s ability to remember the name of the last file you worked makes it unnecessary for you to remember what project you were in the middle of when you pulled the plug and went to bed. Furthermore, NASM-IDE also remembers the exact cursor position where the cursor was when you saved your file and exited, as well as whether the edit window was zoomed. Most of the time, if you’re in the middle of a project and want to get back down to it, you only need to type “NASMIDE” followed by Enter on the DOS command line. If you were working on EAT2.ASM and had it open when you shut NASM-IDE down, you don’t have to type EAT2.ASM again on the command line when you invoke NASM-IDE.

When you create a new file or load a file into the editor for the first time, it becomes, by default, the current file. This means it is the file that will be assembled when you tell NASM-IDE to invoke NASM to translate