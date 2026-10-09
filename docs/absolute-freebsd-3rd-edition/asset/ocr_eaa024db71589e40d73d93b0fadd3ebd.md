Common sense says that you can just copy them to the disk, reboot, and be done with it.

Here’s yet another instance where your common sense is trying to run your mouth. On rare occasions, the FreeBSD team needs to make some low-level changes in the system that require running the install in single-user mode. You can have conflicts where vital programs won’t run when installed in multiuser mode. This is rare, but if it happens with /bin/sh, you’re in a world of hurt. You have a very straightforward recovery route if that happens: remove the hard drive from the server, mount it in another machine, boot the other machine, and copy your data off the destroyed system before formatting and reinstalling. Or, you can boot from the installation media and demonstrate your amazing sysadmin skills.5

Running in multiuser mode can cause other upgrade problems, such as subtle races, symbol issues, and innumerable other headaches. You can choose to upgrade in multiuser mode, but don’t complain if your system has a problem.

It’s perfectly safe to build your new world in multiuser mode. You can even build and install your new kernel in multiuser mode. Once you start installing the userland, however, you must be in single-user mode and running on your upgraded kernel.

# NFS AND UPGRADES

Have a lot of machines to update? Look at NFS, which we discussed in Chapter 13. Build world and all your kernels on a central, fast machine, and then export /usr/src and /usr/obj from that system to your other clients. Running make installkernel and make installworld from those NFS exports saves build time on all your other machines and guarantees that you have the same binaries on all your FreeBSD boxes.