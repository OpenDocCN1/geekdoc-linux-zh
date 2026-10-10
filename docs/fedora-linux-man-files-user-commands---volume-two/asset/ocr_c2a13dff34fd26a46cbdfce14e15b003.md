# EXAMPLES

Print the name of the previous branch:

```
$ git check-ref-format --branch @{-1}
```

Determine the reference name to use for a new branch:

```
$ ref=$(git check-ref-format --normalize "refs/heads/$newbranch") ||
die "we do not like '$newbranch' as a branch name."
```