functions, and sophisticated condition testing. Shell scripts are capable of handling everything from simple one-line commands to something complex as starting up your Fedora or RHEL system.

In fact, as you will read in this chapter, Fedora and RHEL do that. They use shell scripts (`/etc/rc/dc.sysinit` and `/etc/rc`) to check and mount all file systems, set up your consoles, launch all system services, and eventually provide you with your login screen. While there are nearly a dozen different scripts available in Fedora and RHEL, the default is `bash`, the Bourne-Again Shell.

# Executing and debugging shell scripts

One of the primary advantages of shell scripts is that they can be opened in any text editor to see what they do. A big disadvantage is that large or complex shell scripts execute more slowly than compiled programs. There are two basic ways to execute a shell script:

+   - The filename is used as an argument to the shell (as in bash script). In this method, the file does not need to be executable; it just contains a list of shell commands. The shell specified on the command line is used to interpret the commands in the script file. This is most common for quick, simple tasks.
- The script may also have the name of the interpreter specified in the first line of the script preceded by `#!` (as in `#!///bash`), and have its execution bit set using chmod +x. You can then run your script just like any other program in your path by simply typing the name of the script on the command line.

> CROSS-REFERENCE: See Chapter 4 for more details on chmod and read/write/execute permissions.

When scripts are executed in either manner, options to the program may be specified on the command line. Anything following the name of the script is referred to as a command-line argument.

As with writing software, there is no substitute for clear and thoughtful design and lots of comments. The pound sign (#) prefixes comments and can take up an entire line or exist on the same line after script code. It's best to implement more complex shell scripts in stages, making sure the logic is sound at each step before continuing. Here are a few good, concise tips to make sure things are working as expected during testing:

+   - Place an echo statement at the beginning of lines within the body of a loop. That, rather than executing the code, you can see what will be executed without making any changes.
- To achieve the same goal, you place dummy echo statements throughout the code. If these lines get printed, you know the correct logic is being taken.