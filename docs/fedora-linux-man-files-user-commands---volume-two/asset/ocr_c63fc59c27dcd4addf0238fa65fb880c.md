of <i>branch</i>. This option overrides that check.

+   - -k, --**keep**
+       Keep downloaded pack.

+   - --no-tags
+       By default, tags that point at objects that are downloaded from the remote repository are fetched and stored locally. This option disables this automatic tag following. The default behavior for a remote may be specified with the remote.<i>name</i>.tagOpt setting. See (1).

+   - -u, --update-head-ok
+       By default <i>git fetch</i> refuses to update the head which corresponds to the current branch. This flag disables the check. This is purely for the internal use for <i>git pull</i> to communicate with <i>git fetch</i>, and unless you are implementing your own Porcelain you are not supposed to use it.

+   - --upload-pack <i>upload-pack</i>
+       When given, and the repository to fetch from is handled by <i>git fetch-pack</i>, --exec=
+       <i>upload-pack</i> is passed to the command to specify non-default path for the command run on the other end.

+   - --progress
+       Progress status is reported on the standard error stream by default when it is attached to a terminal, unless -q is specified. This flag forces progress status even if the standard error stream is not directed to a terminal.

+   - <i>repository</i>
+       The “remote” repository that is the source of a fetch or pull operation. This parameter can be either a URL (see the section GIT URLS below) or the name of a remote (see the section REMOTES below).

+   - <i>refspec</i>
+       Specifies which refs to fetch and which local refs to update. When no <i>refspec</i>’s appear on the command line, the refs to fetch are read from remote.
+       <i>repository</i>.fetch variables instead (see (1)).

The format of a <i>refspec</i> parameter is an optional plus +, followed by the source ref <i>src</i>, followed by a colon :, followed by the destination ref <i>dst</i>. The colon can be omitted when <i>dst</i> is empty.

tag <i>tag</i> means the same as refs/tags/<i>tag</i>:refs/tags/<i>tag</i>; it requests fetching everything up to the given tag.

The remote ref that matches <i>src</i> is fetched, and if <i>dst</i> is not empty string, the local ref that matches it is fast-forwarded using <i>src</i>. If the optional plus + is used, the local ref is updated even if it does not result in a fast-forward update.