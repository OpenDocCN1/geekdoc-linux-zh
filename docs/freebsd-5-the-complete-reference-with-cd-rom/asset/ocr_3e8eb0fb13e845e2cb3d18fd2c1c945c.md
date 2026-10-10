![](bbox=[0.07, 0.08, 0.92, 0.62])

Figure 6-1. The FreeBSD startup and control process is a somewhat tangled tree of interdependencies.

The kernel doesn’t really control these startup steps, but it’s important for two reasons. First, the kernel controls what program controls the startup sequence. In principle, you could change the kernel to run some program other than init as the first program, thus changing the system’s behavior. Second, the kernel provides critical support features to init, the startup scripts’ init calls, and the programs launched from those startup scripts. This support comes in the form of the same underlying support provided to all running programs.