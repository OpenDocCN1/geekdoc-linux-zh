
meaning of these options from `man journald.conf`, which is conveniently laid out in the same order as the config file.

Use the two tabs from Task 1, or open a second tab if necessary. In the first tab, run `tty`, then save the value it prints out for later.

In the second tab, open `/etc/systemd/journald.conf` for editing as root (via `sudo` or `sudoedit`). Append these two lines to the bottom of the file:

```text
ForwardToConsole=yes

TTYPath=[tty]
```

... where `[tty]` is the value printed by `tty` in the other tab. Save and quit the editor, then run:

- `sudo systemctl restart systemd-journald`
- `systemd-cat echo "Hello World"`

Now look back at the first tab again. You should see logs being printed directly to your console! This can be useful for monitoring system logs, generally, without having to keep a process running.

## Task 3:

Clean up:

- Edit `/etc/systemd/journald.conf` again and delete the two lines you added
- Run `sudo systemctl restart systemd-journald`

### Notes:

When stored persistently on the disk (which is typically what you want to do, as opposed to only storing logs in memory), `journald` logs are stored in `/var/log/journal`. If you try to read these files, however, you will quickly notice that they are not the text logs you may be used to! Somewhat inconveniently, `journald` stores its logs in a binary format which is only readable by systemd-related tools.
