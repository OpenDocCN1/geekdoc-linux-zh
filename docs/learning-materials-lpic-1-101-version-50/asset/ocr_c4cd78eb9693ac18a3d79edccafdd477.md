To kill a session, you can use the command `tmux kill-session -t SESSION-NAME`. If you type the command from within the current, attached session, you will be taken out of `tmux` and back to your initial terminal session:

```
$ tmux kill-session -t "Second Session"
[exited]
$
```

# Sessions Detachment

By killing `Second Session` we were thrown outside `tmux`. However, we still have an active session. Ask `tmux` for a listing of sessions and you will surely find it there:

```
$ tmux ls
LPI: 2 windows (created Tue Aug 27 19:01:49 2019) [158x39]
```

However this session is detached from its terminal. We can attach it with `tmux attach -t SESSION-NAME` (`attach` can be replaced by `at` or — simply — `a`). When there is only a single session, the name specification is optional:

```
$ tmux a
```

You are now back in your session; to detach from it, press `Ctrl + b-d`:

```
[detached (from session LPI)]
$
```

> **TIP**  
> The same session can be attached to more than one terminal. If you want to attach a session making sure it is first detached from any other terminals, use the `-d` switch: `tmux attach -d -t SESSION-NAME`.

Important commands for session attaching/detaching:

+   *   `Ctrl + b-d`
+       select what client to detach.
+   *   `Ctrl + b-r`
+       refresh the client’s terminal.