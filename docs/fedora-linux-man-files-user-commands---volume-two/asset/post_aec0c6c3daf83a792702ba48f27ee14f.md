
Note that `--force` applies to all the refs that are pushed, hence using it with `push.default` set to `matching` or with multiple push destinations configured with `remote.*.push` may overwrite refs other than the current branch (including local refs that are strictly behind their remote counterpart). To force a push to only one branch, use a `+` in front of the refspec to push (e.g., `git push origin +master` to force a push to the `master` branch). See the `<refspec>` section above for details.

### -[repository=<repository>]
- This option is equivalent to the `<repository>` argument. If both are specified, the command-line argument takes precedence.

### -u, --set-upstream
- For every branch that is up to date or successfully pushed, add upstream (tracking) reference, used by argument-less `git pull` and other commands. For more information, see `branch.<name>.merge` in `git-config`.

### --[no-]thin
- These options are passed to `git fetch`. A thin transfer significantly reduces the amount of sent data when the sender and receiver share many of the same objects in common. The default is `--thin`.

### -q, --quiet
- Suppress all output, including the listing of updated refs, unless an error occurs. Progress is not reported to the standard error stream.

### -v, --verbose
- Run verbosely.

### --progress
- Progress status is reported on the standard error stream by default when it is attached to a terminal, unless `-q` is specified. This flag forces progress status even if the standard error stream is not directed to a terminal.

### --recurse-submodules=check|on-demand
- Make sure all submodule commits used by the revisions to be pushed are available on a remote-tracking branch. If `check` is used, Git will verify that all submodule commits that changed in the revisions to be pushed are available on at least one remote of the submodule. If any commits are missing, the push will be aborted and exit with non-zero status. If `on-demand` is used, all submodules that changed in the revisions to be pushed will be pushed. If `on-demand` was not able to push all necessary revisions, it will also be aborted and exit with non-zero status.

### --[no-]verify
- Toggle the `pre-push` hook (see `githooks`). The default is `--verify`, giving the hook a chance to prevent the push. With `--no-verify`, the hook is bypassed completely.

## GIT URLs

In general, URLs contain information about the transport protocol, the address of the remote server, and the path to the repository. Depending on the transport protocol, some of this information may be absent.

Git supports `ssh`, `git`, `http`, and `https` protocols (in addition, `ftp`, and `ftps` can be used for fetching and `rsync` can be used for fetching and pushing, but these are inefficient and deprecated; do not use them).

The native transport (i.e. `git://` URL) does no authentication and should be used with caution on unsecured networks.

The following syntaxes may be used with them:

- `http[s]://host.xz[:port]/path/to/repo.git/`
- `ftp[s]://host.xz[:port]/path/to/repo.git/`

An alternative scp-like syntax may also be used with the ssh protocol:

- `[user@]host.xz:path/to/repo.git/`

This syntax is only recognized if there are no slashes before the first colon. This helps differentiate a local path that contains a colon. For example, the local path `foo:bar` could be specified as an absolute path or `./foo:bar` to avoid being misinterpreted as an ssh url.

The ssh and git protocols additionally support `~username` expansion:

- `[user@]host.xz:~[user]/path/to/repo.git/`

For local repositories, also supported by Git natively, the following syntaxes may be used:

- `/path/to/repo.git/`

These two syntaxes are mostly equivalent, except when cloning, when the former implies `--local` option. See `git-clone` for details.

When Git doesn't know how to handle a certain transport protocol, it attempts to use the `remote-<transport>` remote helper, if one exists. To explicitly request a remote helper, the following syntax may be used:

- `<transport>::<address>`

where `<address>` may be a path, a server and path, or an arbitrary URL-like string recognized by the specific remote helper being invoked. See `gitremote-helpers` for details.

If there are a large number of similarly-named remote repositories and you want to use a different format for them (such that the URLs you use will be rewritten into URLs that work), you can create a configuration section of the form:

```
[url "actual url base"] insteadof  = <other url base>
```

For example, with this:

```
[url ""] insteadOf = host.xz:/path/to/ insteadOf = work:
```

a URL like “`work:repo.git`” or like “`host.xz:/path/to/repo.git`” will be rewritten in any context that takes a URL to be `""`.

If you want to rewrite URLs for push only, you can create a configuration section of the form:

```
    [url "<actual url base>"] pushInsteadOf = <other url base>
```

For example, with this:

```
    [url ""] pushInsteadOf =
```

a URL like `""` will be rewritten to `''` for pushes, but pulls will still use the original URL.

## REMOTES

The name of one of the following can be used instead of a URL as `<repository>` argument: a remote in the Git configuration file: `$GIT_DIR/config`, a file in the `$GIT_DIR/remotes` directory, or a file in the `$GIT_DIR/branches` directory.

All of these also allow you to omit the refspec from the command line because they each contain a refspec which git will use by default.

### Named remote in configuration file

You can choose to provide the name of a remote which you had previously configured using `git remote add`, `git config` or even by a manual edit to the `$GIT_DIR/config` file. The URL of this remote will be used to access the repository. The refspec of this remote will be used by default when you do not provide a refspec on the command line. The entry in the config file would appear like this:

```
    [remote "<name>"] url = <url> pushurl = <pushurl> push = <refspec> fetch = <refspec>
```

The `<pushurl>` is used for pushes only. It is optional and defaults to `<url>`.

### Named file in $GIT_DIR/remotes

You can choose to provide the name of a file in `$GIT_DIR/remotes`. The URL in this file will be used to access the repository. The refspec in this file will be used as default when you do not provide a refspec on the command line. This file should have the following format:

```
    URL: one of the above URL format Push: <refspec> Pull: <refspec>
```

`Push:` lines are used by `git push` and `Pull:` lines are used by `git pull` and `git fetch`. Multiple `Push:` and `Pull:` lines may be specified for additional branch mappings.

### Named file in $GIT_DIR/branches

You can choose to provide the name of a file in `$GIT_DIR/branches`. The URL in this file will be used to access the repository. This file should have the following format:

```
    <url>#<head>
```

`<url>` is required; `#<head>` is optional.

Depending on the operation, git will use one of the following refspecs, if you don’t provide one on the command line. `<branch>` is the name of this file in `$GIT_DIR/branches` and `<head>` defaults to `master`.

`git fetch` uses:
`refs/heads/<head>:refs/heads/<branch>`

`git push` uses:
`HEAD:refs/heads/<head>`

## OUTPUT

The output of “`git push`” depends on the transport method used; this section describes the output when pushing over the Git protocol (either locally or via ssh).

The status of the push is output in tabular form, with each line representing the status of a single ref. Each line is of the form:

```
<flag> <summary> <from> -> <to> (<reason>)
```

If `--porcelain` is used, then each line of the output is of the form:

```
<flag> \t <from>:<to> \t <summary> (<reason>)
```

The status of up-to-date refs is shown only if `--porcelain` or `--verbose` option is used.

### flag

A single character indicating the status of the ref:

- `(space)` for a successfully pushed fast-forward;
- `+` for a successful forced update;
- `-` for a successfully deleted ref;
- `*` for a successfully pushed new ref;
- `!` for a ref that was rejected or failed to push; and
- `=` for a ref that was up to date and did not need pushing.

### summary

For a successfully pushed ref, the summary shows the old and new values of the ref in a form suitable for using as an argument to `git log` (this is `<old>…<new>` in most cases, and `<old>…<new>` for forced non-fast-forward updates).

For a failed update, more details are given:

- `rejected`: Git did not try to send the ref at all, typically because it is not a fast-forward and you did not force the update.
- `remote rejected`:
