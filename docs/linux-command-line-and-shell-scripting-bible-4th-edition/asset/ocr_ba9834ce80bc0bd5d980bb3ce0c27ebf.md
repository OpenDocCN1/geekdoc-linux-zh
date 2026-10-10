# NOTE

A version control system for Linux projects was created by Linus Torvalds in 2005. You may recognize that name, since he developed the Linux kernel (*Chapter 1*, “*Starting with Linux Shells*”). Linus desired a distributed VCS that could quickly merge files as well as provide other features that Linux kernel developers needed. He couldn’t find one, so he wrote one! The result was Git, which is still a very popular high-performance distributed VCS.

Git is a distributed VCS, which is often employed in agile and continuous software development environments. But it is also used for managing Bash shell scripts. To understand Git's underlying principles, you need to know a few terms related to its configuration. *Figure 25-1* shows a conceptual depiction of the Git environment.

Each location within the Git environment is important. The following sections cover the details of these areas and highlight a few special Git features.

# Working directory

The *working directory* is where all the scripts are created, modified, and reviewed. It is typically a subdirectory within the script writer's home directory, similar to /home/christine/scripts. It is best to create a new subdirectory for every project, because Git places files within that location for tracking purposes.