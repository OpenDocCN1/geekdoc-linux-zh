+   1. **-E**  
+      Start **Vim** in improved Ex mode, just like the executable was called “exim”.
+   2. **-f**  
+      Foreground. For the GUI version, **Vim** will not fork and detach from the shell it was started in. On the Amiga, **Vim** is not restarted to open a new window. This option should be used when **Vim** is executed by a program that will wait for the edit session to finish (e.g. mail). On the Amiga the “:sh” and “:!” commands will not work.
+   3. **—nofork**  
+      Foreground. For the GUI version, **Vim** will not fork and detach from the shell it was started in.
+   4. **-F**  
+      If **Vim** has been compiled with FKM support for editing right-to-left oriented files and Farsi keyboard mapping, this option starts **Vim** in Farsi mode, i.e. ‘fkmap’ and ‘rightleft’ are set. Otherwise an error ssgase is given and **Vim** aborts.
+   5. **-g**  
+      If **Vim** has been compiled with GUI support, this option enables the GUI. If no GUI support was compiled in, an error ssgage is given and **Vim** aborts.
+   6. **-h**  
+      Give a bit of help about the command line argunts and options. After this **Vim** exits.
+   7. **-H**  
+      If **Vim** has been compiled with RIGHTLEFT support for editing right-to-left oriented files and Hebrew keyboard mapping, this option starts **Vim** in Hebrew mode, i.e. ‘hkmap’ and ‘rightleft’ are set. Otherwise an error ssgage is given and **Vim** aborts.
+   8. **-i {viminfo}**  
+      When using the viminfo file is enabled, this option sets the filena to use, instead of the default “~/.viminfo”. This can also be used to skip the use of the .viminfo file, by giving the na “NONE”.
+   9. **-L**  
+      Sa as -r.
+   10. **-l**  
+      Lisp mode. Sets the ‘lisp’ and ‘showmatch’ options on.
+   11. **-m**  
+      Modifying files is disabled. Resets the ‘write’ option. You can still modify the buffer, but writing a file is not possible.
+   12. **-M**  
+      Modifications not allowed. The ‘modifiable’ and ‘write’ options will be unset, so that changes are not allowed and files can not be written. Note that these options can be set to enable making modifications.
+   13. **-N**  
+      No-compatbile mode. Reset the ‘compatible’ option. This will make **Vim** behave a bit better, but less Vi compatible, even though a .vimrc file does not exist.
+   14. **-n**  
+      No swap file will be used. Recovery after a crash will be impossible. Handy if you want to edit a file on a very slow dium (e.g. floppy). Can also be done with “:set