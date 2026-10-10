This section gives an elementary overview of SELinux. If you’d like to explore SELinux further, I recommend visiting the NSA website at http://www.nsa.gov/selinux/.

# ## SELinux Architecture

SELinux is more than kernel code. SELinux consists of the kernel code plus related library, files, and administration tools. The system or security administrator creates a security policy for SELinux to use. This policy is then implemented on the system and administered through SELinux tools such as *newrole*, *setfiles*, *checkpolicy*, and a whole host of others.

In addition to the SELinux-specific tools, some standard Linux tools are also modified to work with SELinux, including commands such as *ps*, *ls*, *cron*, and others.

# ### SUBJECTS, OBJECTS, AND ACTIONS, OH MY!

Three elements compose SELinux’s security model: Subjects, Objects, and Actions. Subjects are the protagonists within the context of SELinux; they are the things that work on or perform actions on objects. Objects are, therefore, the items on which subjects act. Examples of objects include files; processes; special devices like block devices, character devices, and sockets; directories; and filesystems. Objects are actually divided into classes of objects and include those listed above plus many more. And, yes, processes can be both subjects and objects. In other words, a process can perform the action or it can have the action performed on it.

> **OBJECT PERSISTENCE**
> Objects are either *persistent* or *transient*. *Persistent objects* are those that are *long-lived*, such as *files*. *Transient objects* are *short-lived*, such as *a process while running*.

Each domain has a limited number of files and operations it can access. Each domain’s definition classifies the operations it can perform on files within a certain class. Processes can also transition into other domains under certain conditions.

When an action is requested, for example, a program attempting to read `/etc/shadow`, an Access Decision must be made. This Access Decision is made based on three security attributes:

+   - User identity
+   - Role
+   - Type