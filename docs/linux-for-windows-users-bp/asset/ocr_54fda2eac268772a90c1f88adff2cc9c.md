function keys two to six. You have to log in again on the new console, but you do not have to log in as a different user. Of course, you only have to log in the first time you switch to it. Thereafter you can switch between consoles without a password.

The -h option tells the computer to reboot, whereas the -r option tells the computer to halt once. The new option in both examples tells Linux to execute the command at once, which is what you normally require when Linux on a workstation.

The alternative is to use a time here.

A session to a console where you can move from one console to another. This gives a form of multi-tasking where you can have (say) a word processor on the scene on one console and a game on the other. If the process arrives at the screen you can almost instantly switch from the game back to the word processor. Of course, with any form of multi-tasking the demands on the computer are increased as more programs are run. In particular, the number of consoles and applications tend to increase dramatically as the number of CPUs and applications in use are increased. With a PC that has a limited amount of memory this factor might restrict the use of multiple consoles.

When you have finished using a virtual console the logout command can be used to switch it off. Pressing the Alt key and a suitable function key then takes the system onto another console. You do not actually have to logout of unused consoles, and they can be left running while you use another. When the system is shutdown, all active consoles will be terminated "cleanly". However a console left running unnecessarily will presumably waste system resources, and should therefore be shutdown.

# Rebooting

# Text editing

As we saw in the previous chapter, the system can be shutdown "cleanly" and immediately using this command:

```
`shutdown -h now`
```

The shutdown command will only work if you log in as "root" incidentally, without root privileges you simply generate an error message. As the shutdown command terminates a session by switching off the computer, you should not leave files open and next time problems occur.

This would leave files open and next time Linux is used it is not shut down properly, and it will go through a lengthy check of the hard disc drive before booting up properly.

There are two options available if a reboot of the computer is required. The easiest way is to employ the `reboot`, `halt` and `poweroff` commands; these are the same method commands used in MS-DOS. The alternative is to use this version of the shutdown command:

```
`shutdown -r now`
```

Under the later versions of MS-DOS it is possible to produce edit text files using the edit command. This is useful for editing files such as the autoexec.bat and config.sys files. In fact you will find it easy to produce or edit files under Linux. You may also find it necessary to be able to go into X Windows and use one of the ".txt" text files. If you prefer to use a traditional text editor there should be both `regedit` and `IV` available on the system. Emacs seems to be generally regarded as the more accomplished of the two and is both capable of handling large text files if necessary. To edit a file called `/root/hello` using `Emacs` and `IV` text files if necessary. Commands would be used:

+   ```bash
+   emacs /root/hello
+   v /root/hello
+   ```
+   

Note that it may be Xemacs rather than Emacs that run if you are using a console from within an X Windows front-end such as KDE. If this should happen, exit to the console in order to run Emacs.

In order to fit in the command. For example, these commands would open an existing file called `/root/goodbye`

+   ```bash
+   emacs /root/goodbye
+   v /root/goodbye
+   ```
+   

Incidentally, a modern version of Linux the `v` command will actually run the improved version of vi called vim by default. Neither of these text editors are much like the MS-DOS "edit" program. But Emacs is probably the easier editor to use if you are used to using text editors. Try making a test file to edit or a similar MS-DOS text editor. Try making a test file to edit or a similar

```
`emacs /root/testfile`
```

Ones into /root/testfile

Emacs and Windows text editors, you can type some text, use the cursor keys to move around the text, and delete text using the Delete and Backspace keys. Text can be freely added to existing text. With MS-DOS and Windows text editors it is normally possible to toggle between