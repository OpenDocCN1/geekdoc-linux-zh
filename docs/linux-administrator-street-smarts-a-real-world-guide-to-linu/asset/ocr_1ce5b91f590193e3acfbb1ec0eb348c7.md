![](bbox=[0.14, 0.1, 0.36, 0.24])

An OS is defined largely by its software. The software isn't static, though; once you've installed a package, you may need to remove it, upgrade it, or replace it with something entirely dif-

ferent. Package management software, such as the RPM Package Manager (RPM) and Debian package tools, help you to do this. In addition to understanding package management, to be truly "street smart" in the Linux world, you should know how to install software from source code. This will enable you to tweak the software in various ways and to install unusual soft- ware that's not available in a binary package for your distribution. Being able to back up your installed software and user files will help you ensure that your system operates smoothly, with minimal downtime.

![](bbox=[0.13, 0.43, 0.22, 0.49])

> Task 3.1 covers RPM and Task 3.2 covers Debian packages. Ordinarily, a single computer runs just one of these two systems, not both, so if you have access to one computer running one Linux distribution, you'll be able to perform only one of these tasks. A few Linux distributions, such as Slackware and Gentoo, use other package management tools, so neither of these tasks applies directly to them.

Even once it's installed, running software needs management—you may need to determine what's running, terminate some running programs, and rein in others that are causing problems. On a bigger scale, you should know how to adjust Linux runlevels, which are sets of system software and servers that you can start or stop all at once. Finally, Linux relies heavily on cron and similar utilities, which enable you to schedule processes to run at particular times in the future. Doing so lets you schedule routine automated tasks, such as checking for available system software upgrades, at convenient times.

![](bbox=[0.13, 0.72, 0.22, 0.78])

> This phase maps to portions of the CompTIA Linux+ objectives 1, 2, and 3 and to portions of the LPIC objectives 102, 103, 106, and 111.

# Task 3.1: Use RPM

RPM is the most popular of the Linux package managers. It enables you to install, upgrade, uninstall, query, and verify the integrity of packages. RPM works on individual package files whose filenames end in .rpm. These files are compressed archive files, similar to compressed