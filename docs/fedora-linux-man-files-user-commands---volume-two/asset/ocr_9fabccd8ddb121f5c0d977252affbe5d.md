# DESCRIPTION

Runs a number of housekeeping tasks within the current repository, such as compressing file revisions (to reduce disk space and increase performance) and removing unreachable objects which may have been created from prior invocations of `git add`.

Users are encouraged to run this task on a regular basis within each repository to maintain good disk space utilization and good operating performance.

Some `git` commands may automatically run `git gc`; see the `—auto` flag below for details. If you know what you're doing and all you want is to disable this behavior permanently without further considerations, just do:

```
$ `git config --global gc.auto 0`
```