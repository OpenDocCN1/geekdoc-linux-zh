
# Operands

file A path name of a file to be edited.

# Usage

The states for the ex command are listed below.

| State | Description |
| --- | --- |
| Command | Normal and initial state. Input prompted for by a colon (:). Your line-kill character cancels a partial command. |
| Insert | Entered by a, i, or c. You can enter arbitrary text. Insert state normally is terminated by a line having only on it, or, normally, with an interrupt. |
| Visual | Entered by typing vi; terminated by typing q or ^\ (Control-\). |
| Abbreviate | ab ab[brev] word rhs |
| Adjust Window | [line] z [type] [count] [flags] |
| Append | a [line] a[append] [!] |
| Arguments | ar [gs] |
| Change | c [range] c[change] [!] [count] |
| Change Directory | chd chd[ir] [directory]; cd[!] [directory] |
| Copy | co [range] co[py] line [flags]; [range] t line [flags] |
| Delete | d [range] d[delete] [buffer] [count] [flags] |
| Edit | e[dic] [!] [+line] [file]; ex[!] [+line] [file] |
| Escape | command [range]! command |
| Execute | @buffer; * buffer |
| File | f f[file] [file] |
| Global | g [range] g[lobal] /pattern/ [commands]; [range] v /pattern/ [commands] |
| Insert | i [line] i[insert] [!] |
| Join | j [range] j[oin] [!] [count] [flags] |

The commands, abbreviations, and command arguments for the ex command are listed below. For /usr/xpg4/bin/ex if you specify both a count and a range for a command that uses them, the number of lines affected is taken from the count value instead of the range. The starting line for the command is taken to be the first line addressed by the range.

# Command Abbreviation Arguments

| Command | Abbreviation | Arguments |
| --- | --- | --- |
| List | l | [range] [ist] [count] [flags] |
| Map | map | map[!] [x rhs] |
| Mark | ma | [line] ma[rk] x; [line] k x |
| Move | m | [range] m[ove] line |
| Next | n | n[ext] [!] file ... |
| Number | nu | [range] nu[mber] [count] [flags]; [range] # [count] [flags] |
| Open | o | [line] o[pen] /pattern/ [flags] |
| Preserve | pre | pre[serve] |
| Print | p | [range] p[rint] [count] [flags] |
| Put | pu | [line] pu[t] [buffer] |
| Quit | q | q[uit] [!] |
| Read | r | [line] r[ad] [!] file |
| Recover | rec | rec[over] file |
| Resubstitute | | [range] & [options] [count] [flags]; [range] s[substitute] [options] [count] [flags]; [range] [options] [count] [flags] |
| Rewind | rew | rew[ind] [!] set[t] [option=[value]]... [noopion-] [option=...] [all] |
| Scroll | | EOF |
| Shell | sh | sh[ell] |
| Shift Left | | [range] < [count] [flags] |
| Shift Right | | [range] > [count] [flags] |
| Source | so | so[ource] file |
| Substitute | s | [range] s[substitute] [/pattern/repl/[options] [count] [flags] |
| Suspend | su | su[pend] [!]; st[op] [!] |
| Tag | ta | ta[g] [!] tagstring |
| Unabbreviate | una | una[bbrev] word |
| Undo | u | u[ndo] |
| Unmap | unm | unm[ap] [!] x |
| Visual | vi | [line] vi[sual] [type] [count] [flags] |

| Command | Abbreviation | Arguments |
|---|---|---||
 Write | w | [range] w[rite] [!] [>] [file]; [range] w[rite] [!] [file]; [range] wc[!] [>] [file] |
| Write and Exit | x | [range] x[it] [!] [file] |
| Write Line Number | | [line] = [flags] |
| Yank | ya | [range] ya[nk] [buffer] [count] |

The commands are listed below.

| Command | Description |
|---|---||
| C | Forced encryption |
| X | Heuristic encryption |
| & | Resubstitute. |
| CR | Print next. |
| > | Right shift. |
| < | Left shift. |
| ^D | Scroll. |
| z | Window. |
| ! | Shell escape. |

> Note — The z command prints the number of logical instead of physical lines. More than one screen of output.

The ex addresses are listed below.

| Address | Description |
|---|---|
| n | Line n. |
| . | Current. |
| $ | Last. |
| + | Next. |
| - | Previous. |
| +n | Next. |
| /pat | Next with pat. |
| ?pat | Previous with pat. |
| 'x | Marked x. |
| ' | Previous. |

The scanning patterns are listed below.

| Pattern | Description |
|---|---|
| ^ | Beginning of line. |
| $ | End of line. |
| | Any character. |
| \< | Beginning of word. |
| \> | End of word. |
| [str] | Any character in str. |
| [^str] | Any character not in str. |
| [x-y] | Any character between x and y. |
| * | Any number of preceding. |

The initialization options are listed below.

| Option | Description |
|---|---|
| columns | horizontal screen size. |
| exinit | first list of ex commands that are executed on startup. The list can contain multiple commands separated by the pipe (|). |
| lines | vertical screen size, used as the number of lines in a screenful and the vertical size in visual mode. |

The mode.

| Option | Description |
|---|---||
| sect | horizontal lines. |
| shiftwidth | automatic splitting. |
| showmode | insert mode. |
| slow | stop during insert. |
| wrapmargin | window. |

The environment variables that affect the execution of ex: COLUMNS, HOME, SHELL, TERM, LC_COLLATE, LC_CTYPE, LC_MESSAGES, and NLPATH.

The following options are listed below.

| Option | Description |
|---|---||
| exrc | in $HOME/.exrc.

The editing defaults to certain configuration options. When you initiate an editing session, ex tries to read the EXINIT environment variable. If it exists, the editor uses the values defined in EXINIT; otherwise, the values set in $HOME/.exrc are used. If $HOME/.exrc does not exist, the default values are used.

To use a copy of .exrc located in the current directory other than $HOME, set the exrc option in EXINIT or $HOME/.exrc. Options in EXINIT can be turned off in a local exrc only if exrc is set in EXINIT or $HOME/.exrc.
