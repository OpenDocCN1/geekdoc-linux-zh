# Advanced Bash-Scripting Guide

```
else
# interactive
...
fi
```

Alternatively, the script can test for the presence of option "i" in the -s flag.

```
case $ - in
*i*) # interactive shell
  ;
  *) # non-interactive shell
  ;
esac # (Courtesy of "UNIX F.A.Q.," 1993)
```

However, John Lange describes an alternative method, using the -i test operator.

```
# Test for a terminal!
fd0 = $stdin
# As we recall, the -t test option checks whether stdin, [-t 0 ]
# or stdout, [-t 1 ], in a script is running in a terminal.
if [ -t $fd ];
then
  echo interactive
else
  echo non-interactive
fi
```

> But, as John points out:
# if [-t 0 ] works when you're logged in locally
# but fails when you invoke the command remotely via ssh.
# So for a true test you also have to test for a socket.

```
if [ -t "$fd" || -p /dev/stdin ];
then
  echo interactive
else
  echo non-interactive
fi
```

+   Scripts may be forced to run in interactive mode with the -i option or with a #!bin/bash -i header. Be aware that this can cause erratic script behavior or show error messages even when no error is present.

# 36.2. Shell Wrappers

A wrapper is a script that embeds a system command or utility, that passes a set of parameters to that command. [125] Wrapping around a complex command-line simplifies invoking it. This is especially useful with sed and awk.

A sed or awk script would normally be invoked from the command-line by a sed -e 'commands' or awk 'commands'. Embedding such a script in a Bash script permits it to make it simple, and makes it reusable. This also enables combining the functionality of sed and awk, for example piping the output of a sed of commands to awk. As a saved executable file, you can then repeatedly it in its original form or modified, without the inconvenience of retyping it on the command-line.

Chapter 36. Miscellany

503