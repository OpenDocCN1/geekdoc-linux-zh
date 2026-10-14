```
git checkout master
```

Let’s change the same line of code using nano:

```
nano readme.txt
```

```
cat readme.txt
```

```
## Welcome to My First Repo
## Learning Git is going well so far.
## I added this line in the update-readme branch.
## It’s windy outside today.
```

Now let’s commit these changes:

```
git add -A
```

```
git commit -m "changed sunny to windy"
```

We’ve now created two commits that directly conflict with each other. On the update-readme branch the last line says It’s cloudy outside today., while on the master branch the last line says It’s windy outside today.. Let’s see what happens when we try to merge update-readme into master.

```
git merge update-readme
```