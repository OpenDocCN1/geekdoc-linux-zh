—[no-]force-with-lease, —force-with-lease=<refname>, —force-with-lease=<refname>::<expect>

Usually, “git push” refuses to update a remote ref that is not an ancestor of the local ref used to overwrite it.

This option overrides this restriction if the current value of the remote ref is the expected value. “git push” fails otherwise.

Imagine that you have to rebase what you have already published. You will have to bypass the “must fast-forward” rule in order to replace the history you originally published with the rebased history. If somebody else built on top of your original history while you are rebasing, the tip of the branch at the remote may advance with her commit, and blindly pushing with —force will lose her work.

This option allows you to say that you expect the history you are updating is what you rebased and want to replace. If the remote ref still points at the commit you specified, you can be sure that no other people did anything to the ref. It is like taking a “lease” on the ref without explicitly locking it, and the remote ref is updated only if the “lease” is still valid.

—force-with-lease alone, without specifying the details, will protect all remote refs that are going to be updated by requiring their current value to be the same as the remote-tracking branch we have for them.

—force-with-lease=<refname>, without specifying the expected value, will protect the named ref (alone), if it is going to be updated, by requiring its current value to be the same as the remote-tracking branch we have for it.

—force-with-lease=<refname>::<expect> will protect the named ref (alone), if it is going to be updated, by requiring its current value to be the same as the specified value <expect> (which is allowed to be different from the remote-tracking branch we have for the refname, or we do not even have to have such a remote-tracking branch when this form is used).

Note that all forms other than —force-with-lease=<refname>::<expect> that specifies the expected current value of the ref explicitly are still experimental and their semantics may change as we gain experience with this feature.

“—no-force-with-lease” will cancel all the previous —force-with-lease on the command line.

-f, —force

Usually, the command refuses to update a remote ref that is not an ancestor of the local ref used to overwrite it. Also, when —force-with-lease option is used, the command refuses to update a remote ref whose current value does not match what is expected.

This flag disables these checks, and can cause the remote repository to lose commits; use it with care.