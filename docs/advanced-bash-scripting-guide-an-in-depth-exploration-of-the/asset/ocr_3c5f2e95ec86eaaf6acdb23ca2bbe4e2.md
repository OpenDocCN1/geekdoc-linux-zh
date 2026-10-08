# Advanced Bash-Scripting Guide

Let us use a modified version of the GetOpt.sh script as an example command. This script accepts a number of command-line parameters, preceded by either a single or double dash. And here is the corresponding completion script, by convention given a filename corresponding to its associated command.

# Example J-1. Completion script for UseGetOpt.sh

```
# file: UseGetOpt-2
# UseGetOpt-2.sh parameter-completion

_UseGetOpt-2 ()  # By convention, the function name
  # starts with an underscore.
  local cur
  # Pointer to current command word.
  # By convention, it's named 'cur' but this isn't strictly necessary.

COMPRELY() # Array variable storing the possible completions.
  cur=${COMP_WORDS[COMP_WORD]}

  case "$cur" in
    COMPRELY=$( compgen -W ' -a -d -f -l -t --help --debug \ --file --log --test --help -' $cur ));
    # Generate the completion matches and load them into $COMPRELY array.
    xx) May add more cases here.
    )
  esac

  return 0

```

complete -F _UseGetOpt-2 -o filenames ./UseGetOpt-2.sh
# Invokes function _UseGetOpt-2.

Now, let's try it.

```
bash2 source UseGetOpt-2
bash$ ./UseGetOpt-2.sh [Tab]
  --aoption --debug --file --help --test
  -d -f -h -1 -t

bash$ ./UseGetOpt-2.sh [Tab]
  --aoption --debug --file --help --log --test
```

We begin by sourcing the completion script. This sets the command-line parameters. [1950]

In the first instance, hitting [Tab] after a single dash, the output is all the possible parameters preceded by one or more dashes. Hitting [Tab] after two dashes gives the possible parameters preceded by two or more dashes.

Now, what is the point of jumping through hoops to enable command-line tab completion? It saves keystrokes. [151]

Resources:

Appendix J. An Introduction to Programmable Completion

812