# ## DESCRIPTION

The command takes various subcommands, and different options depending on the subcommand:

```
    git bisect help git bisect start [--no-checkout] [<bad> [<good>...]] [-
    ] [<paths>...] git bisect bad [<rev>] git bisect good [<rev>...] git
    bisect skip [[<rev>|<range>]...] git bisect reset [<commit>] git bisect
    visualize git bisect replay <logfile> git bisect log git bisect run
    <cmd>...
```

This command uses *git rev-list* —bise*ct* to help drive the binary search process to find which change introduced a bug, given an old “good” commit object name and a later “bad” commit object name.

# ### Getting help

Use “git bisect” to get a short usage description, and “git bisect help” or “git bisect -h” to get a long usage description.

# ### Basic bisect commands: start, bad, good

Using the Linux kernel tree as an example, basic use of the bisect command is as follows:

```
        $ git bisect start $ git bisect bad # Current version is bad $ git
        bisect good v2.6.13-rc2 # v2.6.13-rc2 was the last version # tested
        that was good
```

When you have specified at least one bad and one good version, the command bisects the revision tree and outputs something similar to the following:

```
        Bisecting: 675 revisions left to test after this
```

The state in the middle of the set of revisions is then checked out. You would now compile that kernel and boot it. If the booted kernel works correctly, you would then issue the following command:

```
        $ git bisect good # this one is good
```

The output of this command would be something similar to the following:

```
        Bisecting: 337 revisions left to test after this
```

You keep repeating this process, compiling the tree, testing it, and depending on whether it is good or bad issuing the command “git bisect good” or “git bisect bad” to ask for the next bisection.

Eventually there will be no more revisions left to bisect, and you will have been left with the first bad kernel revision in “refs/bisect/bad”.