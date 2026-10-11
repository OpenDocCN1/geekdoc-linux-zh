![](bbox=[0.05, 0.06, 0.95, 0.51])

Figure 8-1 Using the YaST Sofware Management module

The Sofware Management module allows you to perform a variety of sofware administrative tasks, such as installing, updating, or removing packages. Other distributions provide similar graphical utilities. For example, on Fedora, you can select System | Administration | Add/Remove Sofware from the GNOME desktop to launch the Package Manager graphical utility, shown in Figure 8-2.

These graphical utilities have many advantages. In addition to the easy-to-use interface, most will also automatically detect and resolve package dependencies for you. We'll discuss how dependencies work later in this chapter.

We're not going to spend much time working with these utilities in this chapter. This is done for a variety of reasons. First of all, as with most of the other tasks we've discussed in this chapter, a good Linux admin needs to know how to manage sofware from the command line (really need to understand what's going on ‘under the hood” of the graphical utility (which are usually just graphical front ends for a command-line utility).

In addition, most graphical management utilities can only manage sofware packages. Many of the programs you will install on a Linux system will need to be installed from a source code package. These types of programs must be unttared and compiled. The only way to do this is from the shell prompt. Finally, the LPIC-1/CompTIA Linux+ exam requires you to know how to manage sofware from the shell prompt.