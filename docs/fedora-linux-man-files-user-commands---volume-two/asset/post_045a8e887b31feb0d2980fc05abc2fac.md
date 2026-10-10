
of *branch*. This option overrides that check.

- `-k, --keep`
    Keep downloaded pack.
- `--no-tags`
    By default, tags that point at objects that are downloaded from the remote repository are fetched and stored locally. This option disables this automatic tag following. The default behavior for a remote may be specified with the remote.*name*.tagOpt setting. See (1).
- `-u, --update-head-ok`
    By default *git fetch* refuses to update the head which corresponds to the current branch. This flag disables the check. This is purely for the internal use for *git pull* to communicate with *git fetch*, and unless you are implementing your own Porcelain you are not supposed to use it.
- `--upload-pack *upload-pack*`
    When given, and the repository to fetch from is handled by *git fetch-pack*, --exec=*upload-pack* is passed to the command to specify non-default path for the command run on the other end.
- `--progress`
    Progress status is reported on the standard error stream by default when it is attached to a terminal, unless -q is specified. This flag forces progress status even if the standard error stream is not directed to a terminal.
- `*repository*`
    The “remote” repository that is the source of a fetch or pull operation. This parameter can be either a URL (see the section GIT URLS below) or the name of a remote (see the section REMOTES below).
- `*refspec*`
    Specifies which refs to fetch and which local refs to update. When no *refspec*’s appear on the command line, the refs to fetch are read from remote.*repository*.fetch variables instead (see (1)).

The format of a *refspec* parameter is an optional plus +, followed by the source ref *src*, followed by a colon :, followed by the destination ref *dst*. The colon can be omitted when *dst* is empty.

tag *tag* means the same as refs/tags/*tag*:refs/tags/*tag*; it requests fetching everything up to the given tag.

The remote ref that matches *src* is fetched, and if *dst* is not empty string, the local ref that matches it is fast-forwarded using *src*. If the optional plus + is used, the local ref is updated even if it does not result in a fast-forward update.

**Note** When the remote branch you want to fetch is known to be rewound and rebased regularly, it is expected that its new tip will not be descendant of its previous tip (as stored in your remote-tracking branch the last time you fetched). You would want to use the + sign to indicate non-fast-forward updates will be needed for such branches. There is no way to determine or declare that a branch will be made available in a repository with this behavior; the pulling user simply must know this is the expected usage pattern for a branch.

**Note** There is a difference between listing multiple `<refspec>` directly on `git pull` command line and having multiple remote.<repository>.fetch entries in your configuration for a `<repository>` and running a `git pull` command without any explicit `<refspec>` parameters. `<refspec>`s listed explicitly on the command line are always merged into the current branch after fetching. In other words, if you list more than one remote ref, `git pull` will create an Octopus merge. On the other hand, if you do not list any explicit `<refspec>` parameter on the command line, `git pull` will fetch all the `<refspec>`s it finds in the remote.<repository>.fetch configuration and merge only the first `<refspec>` found into the current branch. This is because making an Octopus from remote refs is rarely done, while keeping track of multiple remote heads in one-go by fetching more than one is often useful.

## GIT URLs

In general, URLs contain information about the transport protocol, the address of the remote server, and the path to the repository. Depending on the transport protocol, some of this information may be absent.

Git supports ssh, git, http, and https protocols (in addition, ftp, and ftps can be used for fetching and rsync can be used for fetching and pushing, but these are inefficient and deprecated; do not use them).

The native transport (i.e. git:// URL) does no authentication and should be used with caution on unsecured networks.

The following syntaxes may be used with them:

- `http[s]://host.xz[:port]/path/to/repo.git/`
- `ftp[s]://host.xz[:port]/path/to/repo.git/`

An alternative scp-like syntax may also be used with the ssh protocol:

- `[user@]host.xz:path/to/repo.git/`

This syntax is only recognized if there are no slashes before the first colon. This helps differentiate a local path that contains a colon. For example the local path foo:bar could be specified as an absolute path or ./foo:bar to avoid being misinterpreted as an ssh url.

The ssh and git protocols additionally support ~username expansion:

- `[user@]host.xz:~[user]/path/to/repo.git/`

For local repositories, also supported by Git natively, the following syntaxes may be used:

- `/path/to/repo.git/`

These two syntaxes are mostly equivalent, except when cloning, when the former implies —local option. See (1) for details.

When Git doesn't know how to handle a certain transport protocol, it attempts to use the remote-<transport> remote helper, if one exists. To explicitly request a remote helper, the following syntax may be used:

- `<transport>::<address>`

where <address> may be a path, a server and path, or an arbitrary URL-like string recognized by the specific remote helper being invoked. See (1) for details.

If there are a large number of similarly-named remote repositories and you want to use a different format for them (such that the URLs you use will be rewritten into URLs that work), you can create a configuration section of the form:

```
[url "actual url base"] insteadof  = <other url base>
```

For example, with this:

```
[url ""] insteadOf = host.xz:/path/to/ insteadOf = work:
```

a URL like “work:repo.git” or like “host.xz:/path/to/repo.git” will be rewritten in any context that takes a URL to be "".

If you want to rewrite URLs for push only, you can create a configuration section of the form:

```
[url "<actual url base>"] pushInsteadOf = <other url base>
```

For example, with this:

```
[url ""] pushInsteadOf =
```

a URL like "" will be rewritten to '' for pushes, but pulls will still use the original URL.

## REMOTES

The name of one of the following can be used instead of a URL as <repository> argument: a remote in the Git configuration file: $GIT_DIR/config, a file in the $GIT_DIR/remotes directory, or a file in the $GIT_DIR/branches directory.

All of these also allow you to omit the refspec from the command line because they each contain a refspec which git will use by default.

### Named remote in configuration file

You can choose to provide the name of a remote which you had previously configured using (1), (1) or even by a manual edit to the $GIT_DIR/config file. The URL of this remote will be used to access the repository. The refspec of this remote will be used by default when you do not provide a refspec on the command line. The entry in the config file would appear like this:

```
[remote "<name>"] url = <url> pushurl = <pushurl> push = <refspec> fetch = <refspec>
```

The <pushurl> is used for pushes only. It is optional and defaults to <url>.

### Named file in $GIT_DIR/remotes

You can choose to provide the name of a file in $GIT_DIR/remotes. The URL in this file will be used to access the repository. The refspec in this file will be used as default when you do not provide a refspec on the command line. This file should have the following format:

```
URL: one of the above URL format Push: <refspec> Pull: <refspec>
```

Push: lines are used by git push and Pull: lines are used by git pull and git fetch. Multiple Push: and Pull: lines may be specified for additional branch mappings.

### Named file in $GIT_DIR/branches

You can choose to provide the name of a file in $GIT_DIR/branches. The URL in this file will be used to access the repository. This file should have the following format:

```
<url>#<head>
```

<url> is required; #<head> is optional.

Depending on the operation, git will use one of the following refspects, if you don’t provide one on the command line. <branch> is the name of this file in $GIT_DIR/branches and <head> defaults to master.
