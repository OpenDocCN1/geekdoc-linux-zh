
sometimes online meetings. In addition, the special versions of the backup script that use encryption also must be modified with the latest changes and tested. This script update project quickly becomes bogged down with complications and required extra communication.

The backup script update project team can get help through version control. *Version control* (also known as *source control* or *revision control*) is a method or system that organizes various project files and tracks updates to them.

> **NOTE**
> **Version control methods or systems can control more than Bash scripts. They can typically handle in-house written software programs, plain-text files, graphics, word processing documents, compressed files, and more.**

A version control system (VCS) provides a common central place to store and merge Bash script files so that the latest version is easily accessed. It protects the files so that a script is not accidentally overwritten by another script writer. And it eliminates extra communications concerning who is currently modifying what.

Additional benefits include situations around new team members of a script project. For example, a new script writer team member can get a copy of the latest backup script version through the version control system and immediately start work on the backup script update project.

*Distributed VCSs* make script projects even easier. The script writers can perform their development or modification work on their own Linux system. Once they've reach a modification goal, they send a copy of their modified files and VCS metadata to the remote central system, and other team members can download this latest project version and conduct tests or work on their modification goal. A side benefit is that now the work is backed up to a central location, which is easily accessible from around the world.

### NOTE

A version control system for Linux projects was created by Linus Torvalds in 2005. You may recognize that name, since he developed the Linux kernel (*Chapter 1*, “*Starting with Linux Shells*”). Linus desired a distributed VCS that could quickly merge files as well as provide other features that Linux kernel developers needed. He couldn’t find one, so he wrote one! The result was Git, which is still a very popular high-performance distributed VCS.

Git is a distributed VCS, which is often employed in agile and continuous software development environments. But it is also used for managing Bash shell scripts. To understand Git's underlying principles, you need to know a few terms related to its configuration. *Figure 25-1* shows a conceptual depiction of the Git environment.

Each location within the Git environment is important. The following sections cover the details of these areas and highlight a few special Git features.

## Working directory

The *working directory* is where all the scripts are created, modified, and reviewed. It is typically a subdirectory within the script writer's home directory, similar to /home/christine/scripts. It is best to create a new subdirectory for every project, because Git places files within that location for tracking purposes.

![Figure 25-1](img/a5025f22e05b92f409563a958cac7312_922_0.png)

**FIGURE 25-1** Conceptual depiction of the Git environment

The script writer's Linux system, where the working directory resides, is typically a local server or laptop, depending on workplace requirements. You could even set up your working environment within a local virtual machine that mimics the script's destination system(s). This is also a wonderful method for testing modified or new scripts, because it protects the destination Linux systems from disruption.

## Staging area

A *staging area* is also called the *index*. This area is located on the same system as the working directory. Bash scripts in the working directory are *registered* into the staging area via a Git command (git add). The staging area employs a hidden subdirectory in the working directory named .git. This required location is created via the git init command.

When scripts are cataloged into the staging area, Git creates or updates script information in an index file, .git/index. The data recorded includes checksums (Chapter 24, "Writing Simple Script Utilities"), time stamps, and associated script filenames.

Besides updating the index file, Git compresses the script file(s) and stores these compressed files as an object(s), also called a *blob*, in a .git/objects/ directory. If a script has been modified, it is compressed and stored as a *new* object in the .git/objects/ directory. Git does not just store script modifications; it keeps a compressed copy of *each* modified script.

## Looking at the local repository

The local repository contains each script file's history. It uses the working directory's .git subdirectory as well. Relationships between the script file versions (called a *project tree*) and commit information are stored as objects in the .git/objects/ directory via a Git command (git commit).

Together the project tree and commit data are called a *snapshot*. Every commit creates a *new* snapshot. However, old snapshots are kept, and they are viewable. Another nice feature is that you can return to a previous snapshot if needed.

## Exploring a remote repository

In the Git configuration, the remote repository is typically a cloud-based location that provides a code hosting service. However, you can set up a code hosting site on another server within your local network to serve as the remote repository. What you use really depends on your project's needs as well as your script management team members' locations.

Prominent remote repositories include GitHub, GitLab, BitBucket, and Launchpad. However, by far, GitHub is the most popular. We use GitHub for our remote repository examples in this book.

## Branching

An additional feature provided by Git, called a *branch*, can help in your various script projects. A branch is an area within a local repository for a particular project section. For example, you can have the primary branch in your script project named *main*, and when you make a modification to the script in the *main* branch, it’s best practice to create a new branch, called something like *modification*, and make the changes to the script there. Once the script changes have been tested, the script in the *modification* branch is often merged back into the primary branch.

The advantage to using this method is that your scripts that reside in the *main* branch stay production-worthy, since the Bash shell scripts that are being modified and tested reside in a different branch. Only when the modified scripts are successfully tested are the scripts merged into the main branch.

## Cloning

Another nice feature of Git is that you can copy a project. This process is called *cloning*. If your team brings on a new member, that individual can clone the script and tracking files from the remote repository and have all they need to start participating in modifying the script.

This feature is also useful for specialized versions of a script. In our earlier scenario, the backup script was modified on a few Linux systems to include encryption. When the backup script update project has completed its modifications, merged them into the primary branch, and pushed the local repository to a remote repository, the team responsible for making the special backup script versions can clone the project. Then they'll have all the pieces needed to add encryption to the improved backup script.

![Figure](img/a5025f22e05b92f409563a958cac7312_924_0.png)

## Using Git for VCS

In case you are not yet sold on the idea of using Git as your version control system for your script projects, we'll try to make our case a little stronger. Using Git as your VCS includes the following benefits:

- **Performance** Git uses only local files to operate, making it faster to employ. The exceptions to this include sending and retrieving files to and from a remote repository.
