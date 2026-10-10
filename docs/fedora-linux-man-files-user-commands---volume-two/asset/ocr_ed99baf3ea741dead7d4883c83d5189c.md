# GIT URLS

In general, URLs contain information about the transport protocol, the address of the remote server, and the path to the repository. Depending on the transport protocol, some of this information may be absent.

Git supports ssh, git, http, and https protocols (in addition, ftp, and ftps can be used for fetching and rsync can be used for fetching and pushing, but these are inefficient and deprecated; do not use them).

The native transport (i.e. `git://` URL) does no authentication and should be used with caution on unsecured networks.

The following syntaxes may be used with them:

`http[s]://host.xz[:port]/path/to/repo.git/`
`ftp[s]://host.xz[:port]/path/to/repo.git/`

An alternative scp-like syntax may also be used with the ssh protocol:

`[user@]host.xz:path/to/repo.git/`

This syntax is only recognized if there are no slashes before the first colon. This helps differentiate a local path that contains a colon. For example the local path `foo:bar` could be specified as an absolute path or `./foo:bar` to avoid being misinterpreted as an ssh url.

The ssh and git protocols additionally support `~username` expansion:

`[user@]host.xz:~[user]/path/to/repo.git/`

For local repositories, also supported by Git natively, the following syntaxes may be used:

`/path/to/repo.git/`

These two syntaxes are mostly equivalent, except the former implies `--local` option.

When Git doesn’t know how to handle a certain transport protocol, it attempts to use the `remote-<transport>` remote helper, if one exists. To explicitly request a remote helper, the following syntax may be used:

`<transport>::<address>`

where `<address>` may be a path, a server and path, or an arbitrary URL-like string recognized by the specific remote helper being invoked. See (1) for details.

If there are a large number of similarly-named remote repositories and you want to use a different format for them (such that the URLs you use will be rewritten into URLs that work), you can create a configuration section of the form:

`[url "<actual url base>"]` `insteadOf = <other url base>`

For example, with this:

`[url "" ]` `insteadOf = host.xz:/path/to/` `insteadOf = work:`