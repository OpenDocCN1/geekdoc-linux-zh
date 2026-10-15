
of the entire project history, called a repository, and full access to all version control facilities. Network access is only needed to share changes among members of the same development team or group.

Git’s distributed nature accommodates many different styles of interaction, or workflows. Individuals can share work directly between their personal repositories. Git is the technology behind the social coding website GitHub, which includes many well-known open-source projects, most notably for the Linux kernel.

We discuss Git and GitHub in an examples-based tutorial presentation. For Git and GitHub, the following subsections will include:

- 1. How Git is used, and how it works on a UNIX system
- 2. A high-level overview of the Git terminology, data structures, objects, and actions
- 3. Illustrations, both graphical and verbal, of the Git staging model, what a directed acyclic graph (DAG) is, and a finer-grained view of the object store contents
- 4. A short and a long example of how to create, edit, branch, and merge branches of a Git repository
- 5. An exploration of GitHub as a remote repository
- 6. Three basic examples of how to use git clone, git push, and git pull to transfer repository contents between a local repository and GitHub

To get the most useful information out of this section, you are encouraged to first read through the high-level background materials in first three subsections. Then do the examples in the subsequent three sections, as many times as necessary to become comfortable using Git and GitHub. Finally, be sure to do all in-chapter exercises and the problem set on Git and GitHub at the end of this chapter.

## 17.5.7.1 What Is Git Used for and How Does It Work?

Git is used to manage one or more source code project repositories, each packaged into its own directory that you create for the source code files in that project. A repository is a database containing all the information needed to archive and manage the revisions and history of a project. In Git, as with most VCSs, a repository archives a complete copy of the entire project, with all of the revisions to it.

needed. All of this repository data is stored at the root of your working directory in a hidden subdirectory named .git.

Simply put, with Git and GitHub, you can manage your source code repositories and work in an independent, collaborative, or integrative management way. A majority of the introductory material we present here is aimed at the independent developer. From a learning point of view, you need to first know how to use Git in an independent way. Then we also show some collaborative workflows, particularly with GitHub. We do not touch on the integrative management techniques and commands of Git or GitHub.

## EXERCISE 17.10

What do you think the role of an integrator of a project would be, in terms of what a revision control system accomplishes for a software development and maintenance program?

## 17.5.7.2 Basic Git Terminology

Following is a glossary of basic Git terminology used throughout our examples. This glossary is partitioned into categories that reflect the basic structure of the Git repository itself.

### 17.5.7.2.1 Top-Level Terminology

Repository: The repository is the working directory, and contains inside of itself the source code files you want to maintain and control, the object store, and the index, as shown in Figure 17.7. The advantage of having the repository self-sufficient inside of its own container is that the container can then be shared locally and globally.

A repository can also be thought of as a collection of commits, each of which is an archive of what the project's working tree looked like at a past date, whether on your machine or someone else's. It also defines HEAD, which identifies the branch or commit the current working tree stemmed from. It contains a set of branches and tags, to identify certain commits by name.

![](img/02e070097d401d3bf7de4bf1c470b267_751_0.png)
