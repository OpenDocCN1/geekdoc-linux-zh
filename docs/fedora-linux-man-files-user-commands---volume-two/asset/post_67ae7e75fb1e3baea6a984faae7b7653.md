
# FILES

If not set explicitly with `--file`, there are four files where *git config* will search for configuration options:

- `$(prefix)/etc/gitconfig`
  System-wide configuration file.
- `$XDG_CONFIG_HOME/git/config`
  Second user-specific configuration file. If `$XDG_CONFIG_HOME` is not set or empty, `$HOME/.config/git/config` will be used. Any single-valued variable set in this file will be overwritten by whatever is in `~/.gitconfig`. It is a good idea not to create this file if you sometimes use older versions of Git, as support for this file was added fairly recently.
- `~/.gitconfig`
  User-specific configuration file. Also called "global" configuration file.
- `$GIT_DIR/config`
  Repository specific configuration file.

If no further options are given, all reading options will read all of these files that are available. If the global or the system-wide configuration file are not available they will be ignored. If the repository configuration file is not available or readable, *git config* will exit with a non-zero error code. However, in neither case will an error message be issued.

The files are read in the order given above, with last value found taking precedence over values read earlier. When multiple values are taken then all values of a key from all files will be used.

All writing options will per default write to the repository specific configuration file. Note that this also affects options like `--replace-all` and `--unset`. *git config* **will only ever change one file at a time.**

You can override these rules either by command-line options or by environment variables. The `--global` and the `--system` options will limit the file used to the global or system-wide file respectively. The `GIT_CONFIG` environment variable has a similar effect, but you can specify any filename you want.

## ENVIRONMENT

`GIT_CONFIG`
Take the configuration from the given file instead of .git/config. Using the “--global” option forces this to ~/.gitconfig. Using the “--system” option forces this to $(prefix)/etc/gitconfig.

`GIT_CONFIG_NOSYSTEM`
Whether to skip reading settings from the system-wide $(prefix)/etc/gitconfig file. See [man 1 git-config] for details.

See also the section called “FILES”.

# EXAMPLES

Given a .git/config like this:

```text
# This is the config file, and # a '#' or ';' character indicates # a
# comment #
; core variables [core] ; Don't trust file modes filemode = false
; Our diff algorithm [diff] external = /usr/local/bin/diff-wrapper
renames = true
; Proxy settings [core] gitproxy=proxy-command for kernel.org
gitproxy=default-proxy ; for all the rest
; HTTP [http] sslVerify [http ""] sslVerify = false cookieFile =
/tmp/cookie.txt
```

you can set the filemode to true with

```text
% git config core.filemode true
```

The hypothetical proxy command entries actually have a postfix to discern what URL they apply to. Here is how to change the entry for kernel.org to "ssh".

```text
% git config core.gitproxy "ssh" "for kernel.org$"
```

This makes sure that only the key/value pair for kernel.org is replaced.

To delete the entry for renames, do

```text
% git config --unset diff.renames
```

If you want to delete an entry for a multivar (like core.gitproxy above), you have to provide a regex matching the value of exactly one line.

To query the value for a given key, do

```text
% git config --get core.filemode
```

or

```text
% git config core.filemode
```

or, to query a multivar:

```text
% git config --get core.gitproxy "for kernel.org$"
```

If you want to know all the values for a multivar, do:

```text
% git config --get-all core.gitproxy
```

If you like to live dangerously, you can replace **all** core.gitproxy by a new one with

```text
% git config --replace-all core.gitproxy ssh
```

However, if you really only want to replace the line for the default proxy, i.e. the one without a “for …” postfix, do something like this:

```text
% git config core.gitproxy ssh "! for "
```

To actually match only values with an exclamation mark, you have to

```text
% git config section.key value '[!]'
```

To add a new proxy, without altering any of the existing ones, use

```text
% git config --add core.gitproxy '"proxy-command" for example.com'
```

An example to use customized color from the configuration in your script:

```text
#!/bin/sh WS=$(git config --get-color color.diff.whitespace "blue
reverse") RESET=$(git config --get-color "" "reset") echo "${WS}your
whitespace color or blue reverse${RESET}"
```

For URLs in http.sslVerify is set to false, while it is set to true for all others:

```text
% git config --bool --get-urlmatch http.sslverify true
% git config --bool --get-urlmatch http.sslverify false
% git config --get-urlmatch http http.cookieFile /tmp/cookie.txt
http.sslverify false
```

## CONFIGURATION FILE

The Git configuration file contains a number of variables that affect the Git commands’ behavior. The .git/config file in each repository is used to store the configuration for that repository, and $HOME/.gitconfig is used to store a per-user configuration as fallback values for the .git/config file. The file /etc/gitconfig can be used to store a system-wide default configuration.

The configuration variables are used by both the Git plumbing and the porcelains. The variables are divided into sections, wherein the fully qualified variable name of the variable itself is the last dot-separated segment and the section name is everything before the last dot. The variable names are case-insensitive, allow only alphanumeric characters and -, and must start with an alphabetic character. Some variables may appear multiple times; we say then that the variable is multivalued.

### Syntax

The syntax is fairly flexible and permissive; whitespaces are mostly ignored. The # and ; characters begin comments to the end of line, blank lines are ignored.

The file consists of sections and variables. A section begins with the name of the section in square brackets and continues until the next section begins. Section names are case-insensitive. Only alphanumeric characters, -, and . are allowed in section names. Each variable must belong to some section, which means that there must be a section header before the first setting of a variable.

Sections can be further divided into subsections. To begin a subsection put its name in double quotes, separated by space from the section name, in the section header, like in the example below:

```text
[section "subsection"]
```

Subsection names are case sensitive and can contain any characters except newline (doublequote " and backslash \ can be included by escaping them as \" and \\, respectively). Section headers cannot span multiple lines. Variables may belong directly to a section or to a given subsection. You can have [section] if you have [section “subsection”], but you don’t need to.

There is also a deprecated [section.subsection] syntax. With this syntax, the subsection name is converted to lower-case and is also compared case sensitively. These subsection names follow the same restrictions as section names.

All the other lines (and the remainder of the line after the section header) are recognized as setting variables, in the form name = value (or just name, which is a short-hand to say that the variable is the boolean “true”). The variable names are case-insensitive, allow only alphanumeric characters and -, and must start with an alphabetic character.

A line that defines a value can be continued to the next line by ending it with a \; the backquote and the end-of-line are stripped. Leading whitespaces after name =, the

remainder of the line after the first comment character # or ;, and trailing whitespaces of the line are discarded unless they are enclosed in double quotes. Internal whitespaces within the value are retained verbatim.

Inside double quotes, double quote " and backslash \ characters must be escaped: use \" for " and \\ for .

The following escape sequences (beside " and \) are recognized: \n for newline character (NL), \t for horizontal tabulation (HT, TAB) and \b for backspace (BS). Other char escape sequences (including octal escape sequences) are invalid.

### Includes

You can include one config file from another by setting the special include.path variable to the name of the file to be included. The included file is expanded immediately, as if its contents had been found at the location of the include directive. If the value of the include.path variable is a relative path, the path is considered to be relative to the configuration file in which the include directive was found. The value of include.path is subject to tilde expansion: ~/ is expanded to the value of $HOME, and ~user/ to the specified user's home directory. See below for examples.

### Example

```text
# Core variables [core] ; Don't trust file modes filemode = false
# Our diff algorithm [diff] external = /usr/local/bin/diff-wrapper
renames = true

[branch "devel"] remote = origin merge = refs/heads/devel

# Proxy settings [core] gitProxy="ssh" for "kernel.org"
gitProxy=default-proxy ; for the rest

[include] path = /path/to/foo.inc ; include by absolute path path = foo
; expand "foo" relative to the current file path = ~/foo ; expand "foo"
in your $HOME directory
```

### Values

Values of many variables are treated as a simple string, but there are variables that take values of specific types and there are rules as to how to spell them.

**boolean**

When a variable is said to take a boolean value, many synonyms are accepted for true and false; these are all case-insensitive.

- `true`
  Boolean true can be spelled as yes, on, true, or 1. Also, a variable defined without = <value> is taken as true.
- `false`
