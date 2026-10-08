# ACTION

1. Here is an example of a long directory listing:
% ls -l -d Example
drwxr-x--- 2 taylor 1024 Sep 30 10:50 Example/

Remember that you must have both read and execute permission for a directory. If you have either read or execute permission but not both, the directory will not be usable (as though you had permission). Write permission, of course, enables the user to alter the contents of the directory or add new files to the directory.

2. The Example directory breaks down for interpretation as shown in Figure 4.4.

# Figure 4.4.

Elements of directory permissions.

![](bbox=[0.469, 0.377, 0.775, 0.675])

![](bbox=[0.173, 0.696, 0.263, 0.773])

> I've never understood the nuances of a directory with read but not execute, or vice versa, and explanations from other people have never proven to be correct. It's okay, because I've never seen a directory on a UNIX system that was anything other than ---, r-x, or rwx.

3. Now try it yourself. The -l flag moves to your home directory, and r-x is Is -l
as shown here:
% ls -l
total 403
drwx------ 2 taylor 512 Sep 30 10:38 Archives/
drwx------ 3 taylor 512 Oct 1 08:23 infollorid/

![](bbox=[0.66, 0.883, 0.135, 0.958])