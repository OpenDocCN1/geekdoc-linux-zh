project.

The distributed VCS utility Git is useful in many ways beyond the needs of script writers. There are many more useful project features available with Git. The ones covered in this chapter will get you started down the right path for managing all the amazing Bash shell scripts you are going to write in your lifetime.

# # Summary

In this chapter, we first set the stage for Git by covering concepts such as VCS. Created by Linus Torvalds, Git provides an amazing distributed VCS that is useful for many things, including managing Bash shell scripts. We also took a look at important Git locations, such as the working directory; the staging area, which is also called the index; and the local and remote repositories. In addition, we touched on the branches and cloning features of Git.

Because many Linux distributions do not have Git installed by default, we stepped through installing the `git` package on both CentOS and Ubuntu. Setting up a working directory for the project was done first for the local configuration. The next part covered how to use the `git init` command, which creates a hidden subdirectory, `.git/`, within the working directory. After that, we demonstrated how to configure local repository options for tracking purposes. Finally, we touched on the remote repository, using GitHub as our example.

The chapter ended with using Git in a practical way. Using a sample Bash shell script, we moved it to the working directory, and then added it to the staging area (index) using the `git add` command. The sample script was next committed to the local repository. This was accomplished by using the `git commit` command. The last step in this process was to move the project files to the remote repository. We used GitHub as our remote repository and sent the project there through the `git push` command.

Thanks for joining us on this journey through the Linux command line and shell scripting. We hope you've enjoyed the expedition and have learned how to get around on the command line, and how to create