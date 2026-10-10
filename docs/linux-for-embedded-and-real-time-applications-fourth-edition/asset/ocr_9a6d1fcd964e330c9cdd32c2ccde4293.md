So where did the name “git” come from? Git is British slang for a stupid or unpleasant person. As Linus explained it, “I’m an egotistical bastard, and I name all my projects after myself. First ‘Linux’, now ‘git’.”

# Introducing git

Git is a *distributed* version control system where clients don’t just check out snapshots of files, they fully mirror the central repository. This is illustrated in *figure 16.2*. Each

![](bbox=[0.24, 0.29, 0.8, 0.61])

checkout is a full backup. So if the central server dies, it can be restored from any of the clients with little or no loss. Git is installed with the development tools in most modern Linux distributions.

*Figure 16.3* shows a typical sequence of *git* commands. You start by getting a copy of a project repository with the `git clone` command. This creates a complete local copy of the project from the currently active branch of the central repository. The `hello-world` project is hundreds of versions of the Hello World program in different languages.
Then you make changes to the project. Just for practice, `cd` to the `c/` directory and edit `c.c` to add a header comment. `git add` adds the changes you’ve made to the *index* in preparation for the next *commit*. The index holds a snapshot of the changes that have been added since the last *commit*. You can invoke `git add` multiple times between commits.