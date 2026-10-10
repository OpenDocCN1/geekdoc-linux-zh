Date: Fri Feb 11 16:50:10 2022 -0500

Initial Production Commit
$

Notice in Listing 27.21 that now within the master branch, the new production tier program, ST-UI.py, is managed. Also notice that the Git logs between the two branches were also merged, as shown by the git log command.

![](bbox=[0.13, 0.25, 0.22, 0.31])

There is another flavor of merging called rebasing. Instead of simply merging the commits and history logs into a single branch, rebasing performs new commits for all the files, which simplifies the history logs. To rebase a project, replace git merge with the git rebase command. Which one you employ is dependent on your organization's development workflow as well as team member preferences.

# Summary

The distributed VCS utility Git is useful in many ways beyond the needs of developers. Understanding how to set up working directories, staging areas, and local and remote repositories is a wonderful skill set. Not only will you be able to use the appropriate lingo with your programmers, you can implement Git for various other useful things to manage your Linux systems.

# Exam Essentials

Describe version control. Version control is a method or system that organizes various project files and protects modifications to them. A distributed VCS allows developers to work offline and independently. The Git VCS provides a working directory, staging area (index), and local repository and uses a remote repository provided by a third party. It is popular due to high performance, maintained modification history, file protection, and decentralization.

Explain how to set up your Git environment. The git package provides the various Git tools used for VCSs. Create a working directory for each project using the mkdir command. The .git/ directory, used by both the staging area and the local repository, is initialized via the git init command. Finally, a third party, such as GitHub, can provide the remote repository to use with the various Git tools.