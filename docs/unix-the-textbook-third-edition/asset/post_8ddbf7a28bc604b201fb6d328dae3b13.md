
## 17.5.7.5 Contents of the Object Store

Now that we have illustrated how the working directory is structured, how commits are staged, and the general layout of a repository as shown in a DAG, we can now take a finer-grained look at the objects contained in the object store. Figure 17.10 shows the four object types that are found in the object store and the relationships between those objects.

Remember from the DAG shown in Figure 17.9 that time flows from left to right and an arrow points from a child to a parent. Starting at the top, we see a rectangle to the right representing the branch name, and another smaller square representing a tag object. The name by default is master, but can be assigned text that is more meaningful. The tag is a shorthand label that might represent the initial release number or version of the software code. The circles represent commits. So this diagram shows two commits. The triangles represent tree objects, which can be thought of as directory or linking information between commits and blobs. Finally, at the bottom are a number of blobs, shown linked to the trees that point to them.

In the next section, we discuss a few examples involving Git and GitHub. Before discussing these examples, we give a brief description of the git command.

### SYNTAX

```
git [options] [option arguments] <command> [<command arguments>]
```

Purpose: A distributed version control system with a rich command set that tracks the content of changes in source code files

### Commonly used commands and command arguments:

| add <file> | Stage a file to the index |
| commit | Take a snapshot of the working tree |
| config --global username "<name>" | Configure a repository global username |
| log --oneline | Display a short log of commits on the current branch |
| init | Initialize a repository in the current directory |
| status | Display the status of a repository |

![](img/02e070097d401d3bf7de4bf1c470b267_756_0.png)

## 17.5.7.6 Examples of Using Git and GitHub

We show a few examples describing how to make use of Git and GitHub. Each example consists of the following:

- 1. Topic covered in the example
- 2. Objectives of the example
- 3. Introductory material for understanding the example
- 4. Git commands used in the example
- 5. Prerequisites for carrying out the example
- 6. Detailed procedure
- 7. Conclusions

### Example 17.1: A Short Introduction to Git

Objectives: To briefly illustrate the Git staging model, and how to see differences between the various states of the parts of the repository.

Introduction: As shown previously, the workflow in Git basically follows a pattern of add, edit, modify, stage, and commit. This is the staging model. In this example, we show the essential Git commands that allow you to do that, repetitively if necessary. As you do more commits you add, in a linear fashion, more nodes on the branch named master downstream, after you create the first node in this example. Earlier commits are called upstream commits. The history of the repository flows downstream from the initial commit to the latest commit. Similar to the UNIX diff command, the four basic forms of the git diff command allow you to examine and compare the files and directories present during different states of the repository.

Git commands referenced: Table 17.1 shows the Git commands, and a brief description of each, that are used in this example. It is arranged in the order presented. Any argument enclosed in < > is a string of text. In order to get a more complete description of all the commands in the table, you can look at the man page for a particular command. For example, man git-status gives you a complete man page for the git status command.

Prerequisites: The following are the prerequisites for carrying out this example:

- 1. Having Git installed on your PC-BSD or Solaris system
- 2. Reading through and doing the in-chapter exercises shown in the previous subsections

Procedure: Do the following steps, in order, to meet the objectives of this example.

- 1. Create a working directory within which your Git repository will exist, and make that the current working directory.

```
% mkdir short-git
```
