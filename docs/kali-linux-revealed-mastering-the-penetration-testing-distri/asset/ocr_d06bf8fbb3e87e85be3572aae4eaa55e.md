tory; apt autoclean (apt-get autoclean) only removes packages that can no longer be down-loaded because they have disappeared from the mirror and are therefore useless.
Aptitude is an interactive program that can be used in semi-graphical mode on the console. It is an extremely robust program that can help you install and troubleshoot packages.
synaptic is a graphical package manager that features a clean and efficient graphical interface.
As an advanced user, you can create files in /etc/apt/apt.conf.d/ to configure certain aspects of APT. You can also manage package priorities, track automatically installed packages, work with several distributions or architectures at once, use cryptographic signatures to validate packages, and upgrade files using the techniques outlined in this chapter.

In spite of the Kali/Debian maintainers' best efforts, a system upgrade isn't always as smooth as we would hope. When this happens, you can look at the Kali bug tracker² and at the Debian bug tracking system³ at https://bugs.debian.org/package to check whether the problem has already been reported. You can also try to downgrade the package or to debug and repair a failed package maintainer script.

+   ²http://bugs.kali.org
+   ³https://bugs.debian.org