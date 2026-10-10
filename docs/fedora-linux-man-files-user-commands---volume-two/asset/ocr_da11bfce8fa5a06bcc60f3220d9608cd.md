# ▶ DISCUSSION ON FORK-POINT MODE

After working on the topic branch created with `git checkout -b topic origin/master`, the history of remote-tracking branch `origin/master` may have been rewound and rebuilt, leading to a history of this shape:

![](bbox=[0.1, 0.16, 0.9, 0.19])

where `origin/master` used to point at commits B3, B2, B1 and now it points at B, and your topic branch was started on top of it back when `origin/master` was at B3. This mode uses the reflog of `origin/master` to find B3 as the fork point, so that the topic can be rebased on top of the updated `origin/master` by:

```
$ fork_point=$(git merge-base --fork-point origin/master topic)
$ git rebase --onto origin/master $fork_point topic
```