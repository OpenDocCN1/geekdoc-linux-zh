logfile      /var/svc/log/network-ssh:default.log
restarter    svc/system/svc/restarter:default
contract_id  65
dependency   require_all/none svc/system/filesystem/local (online)
dependency   optional_all/none svc/system/filesystem/autofs (online)
dependency   require_all/none svc/network/loopback (online)
dependency   require_all/none svc/network/physical (online)
dependency   require_all/none svc/system/cryptosvc (online)
dependency   require_all/none svc/system/utmpx (online)
dependency   require_all/restart file:///localhost/etc/ssh/sshd_config (online)

This command line uses the full FMRI, but since there is only one instance of the service, svcs -l ssh would suffice. The state can assume the following values:

+   - online – enabled and successfully started
+   - disabled – not enabled and not running
+   - degraded – enabled but running with limitations
+   - legacy_run – running; used by the few services that haven’t yet been converted to SMF and that still use traditional init.d scripts
+   - uninitialized – starting up and reading configuration
+   - maintenance – reporting that an error requiring administrative attention has occurred
+   - offline – enabled but off-line because the service is waiting on an unsatisfied dependency or cannot start for some other reason

In addition to the current service status, svcs -l lists the service’s log file location, dependencies, and other essentials.

Dependencies allow the specification of arbitrarily complex relationships among services. This facility essentially replaces the system of numbered startup scripts used by the traditional init system, where a script prefixed with S20 runs before one prefixed with S90.

In the example above, SSH requires local filesystems, network interfaces, cryptography services, utmp, and the existence of the sshd_config file. The filesystem automounter is marked as an optional dependency; SSH will run if the automounter is intentionally off-line (as set by the administrator) or if it is on-line and running.

The svcadm command changes the status of a service. To disable the SSH server (don’t try this remotely!), use

```
solaris$ sudo svcadm disable ssh
```

This example uses the short FMRI for SSH, since it’s unambiguous. The disabling is a persistent change; use svcsadm -t to disable SSH temporarily.

Under the hood, SMF configures services through XML files called manifests and profiles. A manifest describes the properties of a service, such as its dependencies and the instructions for starting and stopping it. Manifest files are stored in the /var/svc/manifest directory. Each instance of a service has its own manifest file.