# gc.aggressiveDepth

The depth parameter used in the delta compression algorithm used by *git gc* — aggressive. This defaults to 250.

# gc.aggressiveWindow

The window size parameter used in the delta compression algorithm used by *git gc* — aggressive. This defaults to 250.

# gc.auto

When there are approximately more than this many loose objects in the repository, git gc --auto will pack them. Some Porcelain commands use this command to perform a light-weight garbage collection from time to time. The default value is 6700. Setting this to 0 disables it.

# gc.autoPackLimit

When there are more than this many packs that are not marked with *.keep file in the repository, git gc —auto consolidates them into one larger pack. The default value is 50. Setting this to 0 disables it.

# gc.autoDetach

Make *git gc* —auto return immediately and run in background if the system supports it. Default is true.

# gc.packRefs

Running *git pack-refs* in a repository renders it uncloneable by Git versions prior to 1.5.1.2 over dumb transports such as HTTP. This variable determines whether *git gc* runs *git pack-refs*. This can be set to *notbare* to enable it within all non-bare repos or it can be set to a boolean value. The default is *true*.

# gc.pruneExpire

When *git gc* is run, it will call *prune* —expire 2.weeks.ago. Override the grace period with this config variable. The value “now” may be used to disable this grace period and always prune unreachable objects immediately.

# gc.pruneWorktreesExpire

When *git gc* is run, it will call *prune* —worktrees —expire 3.months.ago. Override the grace period with this config variable. The value “now” may be used to disable the grace period and prune $GIT_DIR/worktrees immediately.

# gc.reflogExpire, gc.<pattern>.reflogExpire

*git reflog expire* removes reflog entries older than this time; defaults to 90 days. With “<pattern>” (e.g. “refs/stash”) in the middle the setting applies only to the refs that match the <pattern>.

# gc.reflogExpireUnreachable, gc.<ref>.reflogExpireUnreachable