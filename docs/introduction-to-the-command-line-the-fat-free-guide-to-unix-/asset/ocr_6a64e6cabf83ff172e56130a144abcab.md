# history

**Purpose:** Display commands that have recently been executed.

**Usage syntax:** `history [OPTIONS]`

```
$ history 10
686 man uptime
687 cat /etc/hosts
688 ls -l
689 uptime
690 dmeg
691 iostat
692 vmstat
693 ping google.com
694 tracepath google.com
695 history 10
Display 10 lines of command history
```

The **history** command displays a user’s command line history. Executing the **history** command with no arguments will display the entire command line history for the current user. For a shorter list, a number can be specified as an argument. Typing **history 10**, for example, will display the last 10 commands executed by the current user as shown in the above example.

> **Tip**  
> You can execute a previous command using `! [NUM]` where *NUM* is the *line number in history you want to recall*. For example, executing `!687` will rerun the command listed on line 687 in the above example.

In Linux, each user has a file called `.bash_history` in their home directory that contains their command line history. Unix systems typically store history in a file called `.sh_history` or `.history`.

> **Note**  
> *The* *history* *file* *may* *contain* *sensitive* *information* *about* *commands* *you* *have* *recently* *executed*. *Most* *systems* *will* *automatically* *overwrite* *command* *line* *history* *after* *a* *certain* *period*. *To* *manually* *erase* *the* *history* *file* *in* *your* *home* *directory* *type* `> $HOME/. *history` *on* *the* *command* *line*.

**Common usage examples:**

+   *   `history` 
+       Display the entire command line history
+   *   `history [NUM]` 
+       Display the specified number of history items
+   *   `history | grep [PATTERN]` 
+       Search history for the specified pattern