```
git add -A
git commit -m "made readme more personal"
```

Like a local Git repository, remote repositories on GitHub can have multiple branches. Let’s push this commit to the update-readme branch on GitHub:

```
git push origin update-readme
```

```
## Counting objects: 3, done.
## Delta compression using up to 4 threads.
## Compressing objects: 100% (3/3), done.
## Writing objects: 100% (3/3), 630 bytes | 0 bytes/s, done.
## Total 3 (delta 0), reused 0 (delta 0)
## To https://github.com/seankross/my-first-repo.
 git
## * [new branch]      update-readme -> update-readme
```

Notice that we needed to specify which remote we were pushing to since GitHub didn’t previously know about the existence of the update-readme branch. When you perform a git push, only the commits on the current branch are sent to the remote repository. That way you can create local branches that cannot be accessed from the remote repository, unless you explicitly push them to GitHub.

Now let’s go back to the GitHub page for our repository. On the left side of the page you should see a button that says “Branch: master.” Click on that button and a little drop-down menu should appear, as you can see below: