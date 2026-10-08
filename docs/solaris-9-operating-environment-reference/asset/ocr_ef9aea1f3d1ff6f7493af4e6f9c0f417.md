# 726

# Operands

file

The name of the file to be printed. Specify `file` as a path name or as a dash (-) to indicate the standard input. If you do not specify `file`, use the standard input.

# Usage

See `largefile(5)` for the description of the behavior of `lp` when encountering greater than or equal to 2 Gbytes (2***31 bytes).

# Exit Status

+   - 0 Successful completion.

+   - non-zero An error occurred.

# Files

+   - `/var/spool/lp/*` LP print queue.

+   - `$HOME/.printers` User-configurable printer database.

+   - `/etc/printers.conf` System printer configuration database.

+   - `fns_ctx_dir.domain` NIS+ version of `/etc/printers.conf`.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| --- | --- |
| Availability CSI | SUNWpccu Enabled |

> Note — CSI capability assumes that printer names are composed of ASCII characters.

# See Also

cancel(1), enable(1), lpstat(1), mail(1), postprint(1), pr(1), stty(1), lpq(1B), lpr(1B), lprm(1B), ladmin(1M), accept(1M), lpfilter(1M), lpforms(1M), lpmove(1M), lpched(1M), lpshut(1M), lpsystem(1M), lusers(1M), nswitch.conf(4), printers(4), printers.conf(4), terminfo(4), attributes(5), environ(5), largefile(5), standards(5)