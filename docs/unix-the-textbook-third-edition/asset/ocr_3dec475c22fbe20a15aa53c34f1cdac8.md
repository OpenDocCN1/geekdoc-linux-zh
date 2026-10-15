# TABLE 17.2 Git Commands Used

| git init | Create a Git repository in the current directory |
| git status | View the status of each file in a repository |
| git add <file> | Stage a file for the next commit |
| git commit | Commit the staged files with a descriptive message |
| git log | View a repository's commit history |
| git config --global user.name "<name>" | Define the author name to be used in all repositories |
| git config --global user.Email <email> | Define the author e-mail to be used in all repositories |
| git checkout <commit-id> | Move a previous commit into the working directory |
| git tag -a <tag-name> -m "<description>" | Create an annotated tag pointing to the most recent commit |
| git revert <commit-id> | Undo the specified commit by applying a new commit |
| git reset --hard | Reset tracked files to match the most recent commit |
| git clean -f | Remove untracked files |
| git reset --hard / git clean -f | Permanently undo uncommitted changes |
| git branch | List all branches |
| git branch <branch-name> | Create a new branch using the working directory as its base |
| git checkout <branch-name> | Make the working directory and HEAD match the specified branch |
| git merge <branch-name> | Merge a branch into the checked-out branch |
| git branch -d <branch-name> | Delete a branch |
| git rm <file> | Remove a file from the working directory (if applicable) and stop tracking that file |

shows you how to obtain Git help and use the man pages on the system for Git commands.

# 4. Completion of Example 17.1.

Procedure: Do the steps shown, in the order presented, to meet the objectives of this example. This is a long and detailed example. If you make mistakes, which for a beginner not familiar with the commands are inevitable, simply start over again in a new directory that has another name than the one shown in step 1.

+   1. The first step in creating a repository to retain a history of your source code project files is to create a directory within which the repository can exist. We name this directory first-git. Then you can do a very elementary configuration of Git to identify yourself to the system.

```
% mkdir first-git
% cd first-git
% git config --global user.name bob
% git config --global user.Email "your_email_address"
%
```

+   2. Create a C source code file named first.c with the text editor of your choice. Save it in the current working directory, which should be first-git.