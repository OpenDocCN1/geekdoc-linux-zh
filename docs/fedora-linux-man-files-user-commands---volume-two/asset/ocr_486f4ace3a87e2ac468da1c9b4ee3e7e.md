boundary commit, or !TREESAME, it remains. Otherwise, it is replaced with its only parent.

The effect of this is best shown by way of comparing to --full-history with parent rewriting. The example turns into:

```
.-A--M---N--o / / I B D \ / `---------'
```

Note the major differences in N, P, and Q over --full-history:

+   - N’s parent list had I removed, because it is an ancestor of the other parent M. Still, N remained because it is !TREESAME.
+   
+   - P’s parent list similarly had I removed. P was then removed completely, because it had one parent and is TREESAME.
+   
+   - Q’s parent list had Y simplified to X. X was then removed, because it was a TREESAME root. Q was then removed completely, because it had one parent and is TREESAME.

Finally, there is a fifth simplification mode available:

```
--ancestry-path
```

Limit the displayed commits to those directly on the ancestry chain between the “from” and “to” commits in the given commit range. I.e. only display commits that are ancestor of the “to” commit and descendants of the “from” commit.

As an example use case, consider the following commit history:

```
D---E---------F / \ B---C---G---H---I---J / \ A---K---  L -M
```

A regular D..M computes the set of commits that are ancestors of M, but excludes the ones that are ancestors of D. This is useful to see what happened to the history leading to M since D, in the sense that “what does M have that did not exist in D”. The result in this example would be all the commits, except A and B (and D itself, of course).

When we want to find out what commits in M are contaminated with the bug introduced by D and need fixing, however, we might want to view only the subset of D..M that are actually descendants of D, i.e. excluding C and K. This is exactly what the --ancestry-path option does. Applied to the D..M range, it results in:

```
E-----F \ G---H---I---J L -M
```

The --simplify-by-decoration option allows you to view only the big picture of the topology of the history, by omitting commits that are not referenced by tags. Commits are marked as !TREESAME (in other words, kept after history simplification rules described above) if (1) they are referenced by tags, or (2) they change the contents of the paths given on the command line. All other commits are marked as TREESAME (subject to be simplified away).

# ## Commit Ordering