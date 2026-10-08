# C Shell

break resumes execution after the end of the nearest enclosing foreach or while loop. The remaining commands on the current line are executed. You can write multilevelreaks as a list of break commands, all on one line.
- continue continues execution of the next iteration of the nearest enclosing\while or foreach loop.

# Korn Shell

break exits from the enclosed for, while, until, or select loop, any. If you specify n,
then break n.
- continue resumes the next iteration of the enclosed for, while, until, or
loop. If you specify n, resume at the n-th enclosed loop.
csh1 commands that are preceded by one or two asterisks (*) are treated specially
in the following ways:

+   - Variable assignment lists preceding the command remain in effect when the\command completes.
- I/O redirections are processed by variable assignments.
- Errors about a script that contains them.
- Words following a command preceded by ** and that are in the format of a\variable assignment are expanded with the same rules as a variable assignment.
Thus, tilde substitution is performed after the = sign, and word-splitting and
file-name generation are not performed.

# Examples

In the following C shell example, the script continues running the while loop until the
user answers Yes (or yes, y, or Y). When the user does answer yes, the break terminates
twhile loop and, in this case, exits because there are no additional commands to
execute.

```
#!/bin/csh -f
while (1)
  echo "-Finished yet? \"
  set answer = $\$
  if ($answer == [Yy]*) break
ndp
```

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| Availability | SUNWcsu |

# See Also

csh(1), exit(1), ksh(1), select(1), sh(1), until(1), attributes(5)