```
## Initialized empty Git repository in /Users/sea\n/my-first-repo/.git/
```

You’ve just created your first repository! Now let’s create a file and start tracking it.

```
echo "Welcome to My First Repo" > readme.txt
```

Now that we’ve created a file in this Git repository, let’s use git status to see what’s going on in this repository. We’ll be using git status continuously throughout this chapter in order to get information about the status of this Git repository.

```
git status
```

```
## On branch master
##
## Initial commit
##
## Untracked files:
##   (use "git add <file>..." to include in what \
will be committed)
##
##       readme.txt
##
## nothing added to commit but untracked files pr\
esent (use "git add" to track)
```

As you can see readme.txt is listed as an untracked file. In order to let Git know that you want to track this file we need to use git add with the name of the file that we want to track. Let’s start tracking readme.txt: