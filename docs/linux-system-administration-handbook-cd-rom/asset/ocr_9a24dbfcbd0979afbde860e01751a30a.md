# # Linux Boot and Shutdown

What happens when you boot? What happens when you shut down the machine?

Booting Linux is not like starting DOS, but the concepts are somewhat similar.

The first process that Linux kicks off once the kernel has entered memory and the root (/) partition is mounted is init. The init process is always process 1. Killing this process will do the same thing as running halt or shut down. Once init starts, there are a few ways it go based on your installation. We prefer the way RedHat does it (the SVR4 method), so we'll work on that setup. The advantage to the RedHat method is that it's the same as other commercial Operating Systems (OS) such as Solaris 2.x

# ## 2.1 LILO

# ### Configuring the Linux Loader

The LILO program allows you to select a boot partition for your system. If you have multiple operating systems (DOS, Windows 95, Linux, etc.) all on