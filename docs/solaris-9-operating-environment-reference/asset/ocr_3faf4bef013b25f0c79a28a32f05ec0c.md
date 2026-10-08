# pgrep, pkill

example, the following command matches processes whose real group ID is other or
demon.

```
castle%  pgrep -G other, daemon
120
castle%
```

If you specify multiple criteria options, pgrep matches processes whose attributes
match the logical AND of the criteria options. For example, the following command
matches processes whose attributes are (real group ID is other OR daemon) AND (real
user ID is root OR daemon).

```
castle%  pgrep -G other, daemon -U root, daemon
120
castle%
```

pkill functions identically to pgrep except that each matching process is signaled as
by kill(1) instead of displaying its process ID. You can specify a signal name or
number as the first command-line option to pkill.

Both commands match the ERE pattern argument against either the pr_fname or
pr_psargs fields of the /proc/nnnn/psinfo files. The lengths of these strings are
elim according to definitions in sys/procs.h. Patterns that can match string
nger than the current limit may fail to match the intended set of processes.

If the pattern contains ERE metacharacters that are also shell
metacharacters, you may need to enclose the pattern with appropriate shell quotes.

Defunct processes are never matched by either pgrep or pkill.
pgrep or pkill process never considers itself a potential match.

# Options

+   -d delim Specify the output delimiter to be printed between each matching
process ID. If you specify no -d option, the default is a newline
character. The -d option is only valid when specified as an option to
pgrep.

+   -f Match the regular expression pattern against the full process argument
string from the pr_psargs fields of the /proc/nnnn/psinfo
file. If you specify no -f option, match the expression only against the
of the executable file (obtained from the pr_fname field of the
/proc/nnnn/psinfo file).

+   -g pgrplist Match processes whose process group ID is in the given list. If you
include group 0 in the list, interpret it as the process group ID of
pgrep or pkill process.

+   -G gidlist Match processes whose real group ID is in the given list. You can
specify each group ID as either a group name or a numerical group ID.

+   -J projidlist Match processes whose project ID is in the given list. You can
specify each project ID as either a project name or a numerical project
ID. New the Solaris 8 release.