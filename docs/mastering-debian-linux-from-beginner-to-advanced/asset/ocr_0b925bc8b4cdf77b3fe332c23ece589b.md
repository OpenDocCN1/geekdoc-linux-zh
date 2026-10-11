```
sudo do-release-upgrade -d
```

# # Performing a Release Upgrade in Fedora

Fedora uses the `dnf system-upgrade` plugin:

+   1. Install the plugin:

```
sudo dnf install dnf-plugin-system-upgrade
```

+   2. Download the new release packages:

```
sudo dnf system-upgrade download --releasever=XX
```

Replace XX with the version number you're upgrading to.

+   3. Trigger the upgrade process:

```
sudo dnf system-upgrade reboot
```

# ## Post-Upgrade Tasks

+   1. **Check System Status:** Verify that all services are running correctly.