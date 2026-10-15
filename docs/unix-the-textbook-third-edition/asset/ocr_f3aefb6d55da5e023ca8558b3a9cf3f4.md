```
HEAD is now at 74088f6... The initial commit
%

```

# 22.

We can check the status of the repository at this point.

```
% git status
HEAD detached at 74088f6
nothing to commit, working directory clean
%
```

# 23.

All previous steps worked on the master branch, where our second and third commits reside. To retrieve our complete history, we just have to check out this entire branch. This is a very brief introduction to branches, but it's all we need to know to navigate between commits. The following command makes Git update our working directory to reflect the state of the master branch's snapshot. It recreates the second.c and third.c files for us, and the content of first.c is updated as well. We're now back to the current state of the entire commits history of the project.

```
% git checkout master
Previous HEAD position was 74088f6... The initial commit
Switched to branch 'master'
%
```

# 24.

Tags are references to milestones, or releases in a software project. They let developers easily browse and check out important revisions. For example, we can now use the v1.0 tag to refer to the third commit instead of its random ID. To view a list of existing tags, execute git tag without any arguments. So, we can label this a stable version of the C program modules. The -a option tells Git to create an annotated tag, which lets us record our name, the date, and a descriptive message, specified via the -m option. We can finalize it by tagging the most recent commit with a version number as follows:

```
% git tag -a v1.0 -m "Stable version of the software"
%
```

# 25.

Now we can add C modules to the working directory that allow us to experiment, without committing those modules. Use the text editor of your choice to create an experimental C source code file named experiment.c, and save it in the current working directory.

# 26.

Then stage that file.

```
% git add experiment.c
%
```

# 27.

Check on the status of the repository.

```
% git status
On branch master
Changes to be committed:
(use "git reset HEAD <file>..." to unstage)
    new file: experiment.c
%
```