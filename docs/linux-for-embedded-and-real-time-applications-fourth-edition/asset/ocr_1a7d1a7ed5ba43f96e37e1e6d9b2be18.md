![](bbox=[0.28, 0.08, 0.75, 0.35])

OK, let’s create a new branch. Maybe you want to test out some ideas, but don’t want to disturb the production code until you’ve thoroughly tested them. Try it with the `hello-world` project. Execute `git branch testing` followed by `git checkout testing`. The `branch` command creates a new branch called `testing` and the `checkout` command causes `HEAD` to point to the specified branch as illustrated in figure 16.8.

![](bbox=[0.27, 0.54, 0.76, 0.75])

Now make a change to one of the files followed by `git add` and `git commit`. Checkout the master branch and make a change there. That results in the situation of figure 16.9. The branches have diverged. It’s important to realize that whenever you `checkout` a different branch, `git` restores the state of the working directory to the `snapshot` that the branch is currently pointing to.

Eventually you’ll reach the point where you want to merge the `testing` branch back into the master production branch. With the master branch checked out, execute `git merge testing`.