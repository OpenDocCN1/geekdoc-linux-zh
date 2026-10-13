where S is assigned to the single-user mode run level; therefore, answer a is incorrect. You need to be in root or superuser mode to run init; therefore, answer b is incorrect. Because the init 1 command only works in distributions where 1 is assigned to the single-user mode run level, answer d is incorrect.

# Question 11

Answer a is correct. This option matches the format for the append command, which is append="irq,i/o,device". The append command does not work at the LILO boot prompt; therefore, answer b is incorrect. Because the address is wrong (0x320 is already assigned to eth0), answer c is incorrect. Because the format of answer d is wrong, answer d is also incorrect.

# Question 12

Answer b is correct. By definition, rt's home directory is /home/rt. Because you're mounting the CD-ROM on the cdrom directory, you're mounting on a subdirectory of /home/rt. Because /home/cdrom is not a subdirectory of /home/rt, answer a is incorrect. You are not mounting on the /cdrom directory; therefore, answer c is incorrect. Although /mnt/cdrom is a fairly standard location for mounting CD-ROM drives, that is not what you're doing with the stated command. Therefore, answer d is incorrect.

# Question 13

Answer b is correct. The TTY signifies the login virtual terminal. A login from a remote computer includes a p. The only PID on the given list being run by a remote user is 983. Because PID 682 is being run on local virtual terminal tty1, answer a is incorrect. Because PID 1235 is being run on local virtual terminal tty4, answer c is incorrect.

# Question 14

Answer c is correct. The xdm command allows you to start a GUI login screen. The startx command starts the X Window without a login screen; therefore, answer a is incorrect. The X command works like startx in some distributions; therefore, answer b is incorrect. Because the XF86Setup command starts the X Window configuration utility, answer d is incorrect.