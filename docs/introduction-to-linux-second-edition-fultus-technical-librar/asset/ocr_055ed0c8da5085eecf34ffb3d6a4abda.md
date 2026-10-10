# ## Appendix C
Shell Features

This document gives an overview of common shell features (the same in every shell flavour) and differ ing shell features (shell specific features).

# ### C.1 Common features

The following features are standard in every shell. Note that the stop, suspend, jobs, bg and fg commands are only available on systems that support job control.

| Command | Meaning |
|---|---|
| > | Redirect output |
| >> | Append to file |
| < | Redirect input |
| << | "Here" document (redirect input) |
| | | Pipe output |
| & | Run process in background. |
| ; | Separate commands on same line |
| * | Match any character(s) in filename |
| ? | Match single character in filename |
| [1] | Match any characters enclosed |
| ( ) | Execute in subshell |
| ' ' | Substitute output of enclosed command |
| " " | Partial quote (allows variable and command expansion) |
| ' ' | Full quote (no expansion) |
| \ | Quote following character |
| $var | Use value for variable |