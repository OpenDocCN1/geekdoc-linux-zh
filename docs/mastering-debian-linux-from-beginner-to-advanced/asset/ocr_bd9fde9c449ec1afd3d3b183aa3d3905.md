2. **Systemd timers**: Use systemd timers for more flexible scheduling options.

Create a timer file:

```
sudo nano /etc/systemd/system/backup.timer
```

Add the following content:

```
[Unit]
Description=Daily backup timer

[Timer]
OnCalendar=daily
Persistent=true

[Install]
WantedBy=timers.target
```

Create a corresponding service file:

```
sudo nano /etc/systemd/system/backup.service
```

Add the following content:

```

```