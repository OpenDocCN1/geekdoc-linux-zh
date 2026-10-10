Setting this value to —no-tags disables automatic tag following when fetching from remote <name>. Setting it to —tags will fetch every tag from remote <name>, even if they are not reachable from remote branch heads. Passing these flags directly to (1) can override this setting. See options —tags and —no-tags of (1).

# remote.<name>.vcs

Setting this to a value <vcs> will cause Git to interact with the remote with the git-remote-<vcs> helper.

# remote.<name>.prune

When set to true, fetching from this remote by default will also remove any remote-tracking references that no longer exist on the remote (as if the —prune option was given on the command line). Overrides fetch.prune settings, if any.

# remotes.<group>

The list of remotes which are fetched by “git remote update <group>”. See (1).

# repack.useDeltaBaseOffset

By default, (1) creates packs that use delta-base offset. If you need to share your repository with Git older than version 1.4.4, either directly or via a dumb protocol such as http, then you need to set this option to “false” and repack. Access from old Git versions over the native protocol are unaffected by this option.

# repack.packKeptObjects

If set to true, makes git repack act as if —pack-kept-objects was passed. See (1) for details. Defaults to false normally, but true if a bitmap index is being written (either via —write-bitmap-index or repack.writeBitmaps).

# repack.writeBitmaps

When true, git will write a bitmap index when packing all objects to disk (e.g., when git repack -a is run). This index can speed up the “counting objects” phase of subsequent packs created for clones and fetches, at the cost of some disk space and extra time spent on the initial repack. Defaults to false.

# rerere.autoUpdate

When set to true, git-rerere updates the index with the resulting contents after it cleanly resolves conflicts using previously recorded resolution. Defaults to false.

# rerere.enabled

Activate recording of resolved conflicts, so that identical conflict hunks can be resolved automatically, should they be encountered again. By default, (1) is enabled if there is an rr-cache directory under the $GIT_DIR, e.g. if “rerere” was previously used in the repository.

# sendemail.identity

A configuration identity. When given, causes values in the *sendmail.identity*.