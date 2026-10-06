# TMUX(1) BSD General Commands Manual TMUX(0/8)

```
NAME
tmux - terminal multiplexer
SYNOPSIS
tmux [-28lquVV] [-c shell-command] [-f file] [-i socket-name]
  -s socket-path] [command flags]
```

DESCRIPTION
tmux is a terminal multiplexer: it enables a number of terminals to be created, accessed, and controlled from a single screen. tmux may be detached from a screen and continue running in the background, later reattached.

When is started it creates a new session with a single window and displays it on screen. A status line at the bottom of the screen shows information on the current session and is used to enter interactive commands:

+   A session of pseudo terminals under the management page tmux(1) line 1 (press h for help or q quit)

```
[PaneDemo] 0:Window* ~:  @linuxbox:~ 19:02 19-Mar $
```

Text marked for copying, we return to normal mode by typing “q”. Now we can paste the copy text by typing Ctrl-b j.

# Detaching Sessions

With tmux it's easier to manage multiple sessions than with screen. First, we can give sessions descriptive names, after creation, as we saw with our “PaneDemo” example above, or by renaming an existing session Ctrl-b s. Second, it's easy to switch sessions on-the-fly by typing Ctrl-b s and choosing a session from the presented list.

While we are in a session, we can use Ctrl-b d to detach it, and into the background. This is useful if we want to create a new session by entering the tmux command.

If we start a new terminal (or log in a remote terminal) and wish to attach an existing session to it, we can use the command tmux ls to display a list of available sessions. To attach a session, we enter the command tmux attach -d t <session_name>. The “d” option causes the session to be detached from its previous terminal and the new terminal. If only one session is running, a tmux attach will connect to it and leave any existing connections intact.

10 Terminal Multiplexers