Imdiately reboots the machine.

# SIGRTMIN+16

Imdiately reboots the machine with kexec.

# SIGRTMIN+20

Enables display of status ssgaes on the console, as controlled via systemd.show_status=1 on the kernel command line.

# SIGRTMIN+21

Disables display of status ssgaes on the console, as controlled via systemd.show_status=0 on the kernel command line.

# SIGRTMIN+22, SIGRTMIN+23

Sets the log level to “debug” (or “info” on **SIGRTMIN+23**), as controlled via systemd.log_level=debug (or systemd.log_level=info on **SIGRTMIN+23**) on the kernel command line.

# SIGRTMIN+24

Imdiately exits the manager (only available for --user instances).

# SIGRTMIN+26, SIGRTMIN+27, SIGRTMIN+28

Sets the log level to “journal-or-kmsg” (or “console” on **SIGRTMIN+27**, “kmsg” on **SIGRTMIN+28**), as controlled via systemd.log_target=journal-or-kmsg (or systemd.log_target=console on **SIGRTMIN+27** or systemd.log_target=kmsg on **SIGRTMIN+28**) on the kernel command line.