the changes we made in the update-readme branch with the master branch. Git incorporates other branches into the current branch by default. When you're merging, the current branch is also called the base branch. Let's switch to the master branch so we can merge in the changes from the update-readme branch:

```
git checkout master
```

```
## Switched to branch 'master'
```

To merge in the changes from another branch we need to use git merge and the name of the branch:

```
git merge update-readme
```

```
## Updating adef548..d7946e9
## Fast-forward
## readme.txt | 2 ++
## 1 file changed, 2 insertions(+)
```

```
cat readme.txt
```