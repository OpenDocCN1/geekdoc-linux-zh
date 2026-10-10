```
git fetch <project> master:test-apply
$ git checkout test-apply
$ git reset --hard
$ git am a.patch
```

If it does not apply correctly, there can be various reasons.

The patch itself does not apply cleanly. That is *bad* but does not have much to do with your MUA. You might want to rebase the patch with (1) before regenerating it in this case.

The MUA corrupted your patch; “am” would complain that the patch does not apply. Look in the .git/rebase-apply/ subdirectory and see what *patch* file contains and check for the common corruption patterns mentioned above.

While at it, check the *info* and *final-commit* files as well. If what is in *final-commit* is not exactly what you would want to see in the commit log message, it is very likely that the receiver would end up hand editing the log message when applying your patch. Things like “Hi, this is my first patch.\n” in the patch e-mail should come after the three-dash line that signals the end of the commit message.