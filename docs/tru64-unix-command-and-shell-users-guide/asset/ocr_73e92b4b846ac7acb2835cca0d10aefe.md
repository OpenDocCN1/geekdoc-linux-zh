# ## Using the System V Habitat

This chapter describes the System V habitat, commands, subroutines and system calls. The commands described in this chapter will enable you to:

+   - Set up your System V habitat environment
+   - Access the System V habitat
+   - Use System V habitat commands

The System V habitat consists of alternate versions of commands, subroutines, and system calls that support the source code interfaces and runtime behavior for all components of the Base System and Kernel Extension as defined in the System V Interface Definition (SVID). This implementation of the System V habitat supports all SVID 2 functions and SVID 3 functions. The System V habitat does not contain alternate versions of default system commands, subroutines, and system calls that already meet the SVID requirement.

Using the System V habitat lets you override the default system commands and functions with corresponding System V commands and functions (system calls and subroutines). You can access the habitat in two ways:

+   - Specify the absolute paths of the System V commands and libraries.
+   - Define the PATH environment variable to search the System V habitat for commands before it searches the default system locations. To set your PATH environment variable, modify your `.profile` or `.login` and `.cshrc` files as described in Section 9.1.

Because the System V system calls are not layered over the system calls in the default system, applications that are built using the system calls in the System V habitat run with virtually no performance overhead. Figure 9–1 illustrates the System V habitat placement within the default operating system and shows that the System V system calls reside at the kernel level.