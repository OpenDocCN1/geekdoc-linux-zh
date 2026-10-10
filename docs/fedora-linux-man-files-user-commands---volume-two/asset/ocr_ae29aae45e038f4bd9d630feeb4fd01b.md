from git-push and updating refs.

receive.shallowUpdate

If set to true, .git/shallow can be updated when new refs require new shallow roots. Otherwise those refs are rejected.

remote.pushDefault

The remote to push to by default. Overrides branch.<name>.remote for all branches, and is overridden by branch.<name>.pushRemote for specific branches.

remote.<name>.url

The URL of a remote repository. See (1) or (1).

remote.<name>.pushurl

The push URL of a remote repository. See (1).

remote.<name>.proxy

For remotes that require curl (http, https and ftp), the URL to the proxy to use for that remote. Set to the empty string to disable proxying for that remote.

remote.<name>.fetch

The default set of “refspec” for (1). See (1).

remote.<name>.push

The default set of “refspec” for (1). See (1).

remote.<name>.mirror

If true, pushing to this remote will automatically behave as if the —mirror option was given on the command line.

remote.<name>.skipDefaultUpdate

If true, this remote will be skipped by default when updating using (1) or the update subcommand of (1).

remote.<name>.skipFetchAll

If true, this remote will be skipped by default when updating using (1) or the update subcommand of (1).

remote.<name>.receivepack

The default program to execute on the remote side when pushing. See option — receive-pack of (1).

remote.<name>.uploadpack

The default program to execute on the remote side when fetching. See option — upload-pack of (1).

remote.<name>.tagOpt