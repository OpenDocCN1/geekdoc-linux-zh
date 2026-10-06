# Linux Administration: A Beginner's Guide

Linux/UN was designed from the ground up to be a multiuser operating system. But a multiuser operating system would not be much good without users! And this brings us to the topic of managing users in Linux.

On computer systems, a system administrator sets up user accounts, determine who has access to. The ability of a person to access a system is determined by whether that user exists and has the proper permissions to use the system.

Associated with each user is "baggage," which can include files, processes, resources, and other information. When dealing with a multiuser system, a system administrator needs to understand what constitutes a user (and the user's baggage) and a group, how they interact together, and how they affect available resources.

In this chapter, we will examine the technique of managing users on a single host. We'll begin by exploring the account database files that contain information about users. From there, we will examine the system tools available to manage the files automatically.

# What Exactly Constitutes a User?

Under Linux, every file and program must be owned by a user. Each user has a unique identifier called a user ID (UID). Each user must also belong to at least one group—a collection of users. Users may belong to multiple groups. Like users, groups also have unique identifiers, called group IDs (GIDs).

The accessibility of a file or program is based on UIDs and GIDs. A running program inherits the rights and permissions of the user who invokes it. (An exception is SetUID and SetGID programs, discussed in "Understanding SetUID and SetGID Programs" in this chapter).

Each user's rights can be defined in one of two ways: as a normal user or a superuser. Normal users can access only what they own or have been given permission to run; permission is granted because the user belongs to the file's group or programs in the system, whether or not he owns the them. A superuser is allowed to access all files and programs. A superuser is a classic example of a superuser and the two words are used interchangeably.

If you are accustomed to Windows, you can draw parallels between system's user management and Linux's user management. Linux UIDs are comparable to Windows SIDs (security identifiers). In contrast to Microsoft Windows, you might find the Linux security model maddeningly simple: Either you're root or you're not.

Normal users do not have root privileges in the same way normal users can be granted administrator access under Windows. Although this approach is a little common, you can implement finer grained access control through the use of access control lists (ACLs) in Linux, as you can with Windows. Which system is better? Depends on what you want and whom you ask.