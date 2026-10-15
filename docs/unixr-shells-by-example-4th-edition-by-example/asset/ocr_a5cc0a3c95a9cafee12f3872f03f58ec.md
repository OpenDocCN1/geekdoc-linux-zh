# EXPLANATION

+   1. The `onintr` command is followed by a label name. The label finish is a user-defined label; control will be transferred to the label if an interrupt occurs. Usually this line is at the beginning of the script. It is not in effect until it is executed in the script.
+   2. The rest of the script lines are executed unless `^C` (Interrupt key) is pressed while the program is in execution, at which time, control is transferred to the label.
+   3. This is the label; when the interrupt comes in, the program will continue to run, executing the statements below the label.
+   4. To shield this part of the script from further interrupts, the `onintr -` is used. If `^C` is entered now, it will be ignored.
+   5. This line is echoed to the screen.
+   6. All tmp files are removed. The tmp files are prefixed with the shell's PID (`$$`) number and suffixed with any number of characters. The program exits with a status of 1.

# 10.9 setuid Scripts

Whoever runs a setuid program temporarily (as long as he or she is running the setuid program) becomes the owner of that program and has the same permissions as the owner. The passwd program is a good example of a setuid program. When you change your password, you temporarily become root, but only during the execution of the passwd program. That is why you are able to change your password in the /etc/passwd (or /etc/shadow) file, which normally is off-limits to regular users.

Shell programs can be written as setuid programs. You might want to do this if you have a script that is accessing a file containing information that should not be accessible to regular users, such as salary or other personal information. If the script is a setuid script, the person running the script can have access to the data, but it is still restricted from others. A setuid program requires the following steps:

+   1. In the script, the first line is
+   
+      ```sh
+      #!/bin/csh -feb
+      ```
+   
+      where the `-feb` options are
+   
+      ```text
+      -f  fast start up; don't execute .cshrc
+      -e  abort immediately if interrupted
+      -b  this is a setuid script
+      ```

+   2. Next, change the permissions on the script so that it can run as a setuid program:
+   
+      ```sh
+      % chmod 4755 script_name
+      or
+      % chmod +sRx script_name
+      % ls -l
+      -rwsr-xr-x  2 ellie       512 Oct 10 17:18 script_name
+      ```