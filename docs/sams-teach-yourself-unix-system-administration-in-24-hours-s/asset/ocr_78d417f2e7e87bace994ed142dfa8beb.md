One of the challenges of multiuser systems is file permission, and a popular research operating system at the time that had gained considerable attention at Bell Telephone Labs (BTL) was Multics. Developed originally by BTL, the Massachusetts Institute of Technology, and General Electric (BTL later dropped out of the project), Multics was an astonishingly complex multuser system that had a highly sophisticated security model, based on concentric circles of access to files, peripherals, and applications.

Brian Kernighan and Ken Thompson, the inventors of the Unix system, had helped with Multics before BTL quit, and although they liked many of its capabilities, they disliked its complexity. The Unix security model, therefore, has an approximately similar concept of circles of access, but in a much simpler manner.

> It's worth mentioning that the name Unix is a bit of a poke at Multics. UN-IX, MULTI-ICS. The saying at Bell Labs used to be "Unix is one of whatever Multics was many of." Learn more, if you're curious, at http://www.multicians.org/

On first glance, the Unix security model seems to be three levels of access: owner, group, and everyone else. A glimmer of how this can be more complex was suggested earlier when I used the id command and learned that I was in two groups, not one. Therefore, although files, programs, or directories can only have a single owner and group, a user can be a member of many groups and thereby end up with access privileges that represent the union of all the individual permissions.

> It's not entirely true that files can only have one owner and group. Creating a hard link to a file can enable the new name to be assigned a different owner and/or group. Yet there's still only one file on the system, so no additional disk space has been consumed. This is a very important concept for system administrators who are going to develop more sophisticated access control methods on their system.

For our purposes, let's start by exploring standard Unix groups, then go from there.

# Task 4.3: Groups and the /etc/group file

Every user account is assigned what's called a default group. On many modern Unix systems, the use of groups has become so uncommon that by default every user gets his own group, effectively negating a powerful characteristic of the Unix operating system itself.