```
```text
[
[ $RETVAL -eq 0 ] && touch /var/lock/subsys/smb || \
RETVAL=1
return $RETVAL
}

stop() {
    KIND="SMB"
    echo -n "${KIND} Shutting down ${KIND} services: "
    killproc smbd
    RETVAL=$?
    echo
    [ $RETVAL -eq 0 ] && rm -f /var/lock/subsys/smb
    return $RETVAL
}

restart() {
    stop
    start
}
```

```

To illustrate the essence of what this script does, I skipped some of the beginning and end of the script (where it checked if the network was up and running and set some values). Here are the actions `smb` takes when it is run with `start` or `stop`:

+   *   **start** — This part of the script starts the `smbd` server when the script is run with the start option.
+   *   **stop** — When run with the `stop` option, the `/etc/init.d/smb` script stops the `smbd` server.

The `restart` option runs the script with a `stop` option followed by a `start` option. If you want to start the `smb` service yourself, type the following command (as root user):

```
```text
# service smb start
Starting SMB services:           [  OK  ]
```
```

To stop the service, type the following command:

```
```text
# service smb stop
Shutting down SMB services:     [  OK  ]
```
```

The `smb` run-level script is different from other run-level scripts in that it supports several other options than `start` and `stop`. For example, this script has options (not shown in the example) that allow you to reload the `smb.conf` configuration file (`reload`) and check the status of the service (`status`).