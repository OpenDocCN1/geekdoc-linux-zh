# EXAMPLE 7.44

```
1 $ cat << DONE
> Hello there
> what's up?
> Bye now The time is `date`.
2 > DONE
Hello there
what's up?
Bye now The time is Thu Oct 28 19:48:23 PST 2004.
$
```

# EXPLANATION

+   1. The cat program accepts input until DONE appears on a line by itself. The << operator allows the input and final terminator to be preceded by one or more tabs.
+   2. The final matching terminator, DONE, is preceded by a tab. The output of the cat program is displayed on the screen.

# 7.12.1 Now What?

Now that we have completed our discussion on the interactive shell, it is time to combine many of these features in scripts, to produce programs that will automate repetitive tasks, produce information, monitor processes, and so on. If you are not a programmer, writing shell scripts may be a good place for you to start. It's fun and you get results quickly.