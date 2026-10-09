# # 14
# EXPLORING /ETC

![](bbox=[0.41, 0.22, 0.59, 0.35])

The /etc directory contains the basic configuration information needed to boot a Unix-like system. Every time I get saddled with an unfamiliar system, one of the first things I do is scope out /etc. The fastest way to go from a junior sysadmin to a midgrade one is to read /etc and the associated man pages. Yes, all of it. Yes, this is a lot of reading. Understanding /etc means that you understand how the system hangs together. As you progress as a sysadmin, you're going to pick up this information piecemeal anyway, so you might as well take the easier route and master this part of your toolkit at the beginning.

I discuss many /etc files in chapters where they're most important, such as /etc/services in Chapter 7 and /etc/fstab in Chapter 10. Also, some files are of only historical interest or are gradually being removed. This chapter covers important /etc files that don't quite fit anywhere else.

# ## /etc Across Unix Species

Different Unix-like systems use different /etc files. In many cases, these files are simply renamed or restructured files from primordial BSD. The first time I encountered an IBM AIX system, for example, I went looking for a BSD-style /etc/fstab. It wasn't there. A little hunting led me to /etc/filesystems, which is an IBM-specific /etc/fstab. Apparently IBM felt that a file named for an abbreviation of filesystem table was confusing, so