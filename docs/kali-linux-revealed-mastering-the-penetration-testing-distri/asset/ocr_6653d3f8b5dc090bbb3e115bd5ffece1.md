If you find an existing bug report, subscribe to it and possibly add supplementary information. Do not post comments such as “Me too” or “+1”; they serve no purpose. But you can indicate that you are available for further tests if the original submitter did not offer this.

If you have not found any report of your problem, go ahead and file it. If you have found related tickets, be sure to mention them.

# Ensure You Use the Latest Version It is very frustrating for developers to receive bug reports for problems that they have already solved or problems that they can’t reproduce with the version that they are using (developers almost always use the latest version of their product). Even when older versions are maintained by the developers, the support is often limited to security fixes and major problems. Are you sure that your bug is one of those?

That is why, before filing a bug report, you should make sure that you are using the latest version of the problematic system and application and that you can reproduce the problem in that situation.

If Kali Linux does not offer the latest version of the application (neither in kali-rolling nor in kali-bleeding-edge, see section 8.1.3.3, “The Kali-Bleeding-Edge Repository” [page 174]), you have alternative solutions: you can try a manual installation of the latest version in a throw-away virtual machine, or you can review the upstream ChangeLog (or Git commit history) to see that there hasn’t been any change that could fix the problem that you are seeing (and then file the bug even though you did not try the latest version).

# Do Not Mix Multiple Issues in a Single Bug Report File one bug report per issue. That way, the subsequent discussions do not get too messy and each bug can be fixed according to its own schedule. If you don’t do that, either the single bug needs to be re-proposed multiple times and can only be closed when all issues have been fixed, or the developers must file the supplementary reports that you should have created in the first place.

# 6.3.2. Where to File a Bug Report

To be able to decide where to file the bug report, you must have a good understanding of the problem and you must have identified in which piece of software the problem lies.

Ideally, you track the problem down to a file on your system and then you use dpkg to find out which package owns that file and where that package comes from. Let’s assume that you found a bug in a graphical application. After looking at the list of running processes (the output of ps aux$), you discovered that the application was started with the /usr/bin/sparta executable:

```
`$ dpkg -S /usr/bin/sparta` 
`sparta: /usr/bin/sparta` 
`$ dpkg -s sparta | grep ^Version:` 
`Version: 1.0.1+git20150729-0kali1`
```

You learn that /usr/bin/sparta is provided by the sparta package, which is in version 1.0.1+git20150729-0kali1. The fact that the version string contains kali indicates to you that the package