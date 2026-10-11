![](bbox=[0.08, 0.09, 0.64, 0.52])

continue the installation in the GUI. You can also write the env parameters to a file and then include it by typing:

```
`--env-file /path/to/<file>`
```

# Setup

The setup described here works fine for using Nextcloud on your home network. In this simple scenario, all the containers run in a single pod. If you want to access the pod from outside your home network, you will need additional containers. TLS encryption for security purposes can be implemented via the Traefik proxy, using HTTPD, NGINX, or Caddy, among others.

If you include Podman as a systemd service, you can simplify image updates via `podman auto-update [9]` by additionally specifying `label=10.containers.autoupdate=image` and using

```
`podman generate systemd --new`
```

> **Listing 4: Podman Configuration**
> 
> `/usr/share/containers/containers.conf`
> `/etc/containers/containers.conf`
> `${HOME}/.config/containers/containers.conf`

![](bbox=[0.08, 0.53, 0.94, 0.93])