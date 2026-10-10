# ## Checking the CHAP-Secrets or PAP-Secrets File

PPP supports two authentication protocols in CentOS: Challenge Handshake Authentication Protocol (CHAP) and Password Authentication Protocol (PAP). Here is what each protocol does to authenticate:

+   * **CHAP** — The server sends the client a challenge packet that includes the server name. The client sends back a response that includes its name and a value that combines the secret and the challenge. The client name and secret are stored in your `/etc/ppp/chap-secrets` file.
+   * **PAP** — The client sends its name and a password (in clear text) for authentication. The client name and secret are stored in your `/etc/ppp/pap-secrets` file.

By default, PPP will authenticate if the server requests it, unless it has no secrets to share. If it has no secrets, PPP (or, more specifically, the PPP daemon `pppd`) will refuse authentication. It is likely that you will find the usernames and passwords you provided when you set up your PPP connection in both of these files. (PPP assumes that you may be using CHAP or PAP authentication.)

The CHAP-secret and PAP-secret formats are the same. Each authentication line can contain the client name, the server name, and the secret. The server name can be represented by an `*` (to allow this secret to be used to authenticate any server). This is useful if you don’t know what the server name will be. Also, remember that case is significant (i.e., `Myserver` is not the same as `myserver`).

> > **TIP**
> > For more about PAP and CHAP in PPP for Linux, type `man pppd` to see the `pppd` man page.

In any case, here’s an example of what a CHAP-secrets file may look like:

```
```
# Secrets for authentication using CHAP
# client        server        secret        IP addresses
######  rechat-config-network will overwrite this part!!! (begin)
######
"abcusername"    "ppp0"     "MySecretPassword"
```
```

> > **WARNING**
> > The PAP-secrets and CHAP-secrets files should not be accessible by anyone but the `root` user. Anyone gaining this information could use it to access your Internet account. By default, permissions are closed to all but the `root` user. To close permission, type `chmod 600 /etc/ppp/*-secrets`.

# ## Looking at the ifcfg File

The ifcfg file for your PPP connection is stored in a filename that includes the provider name you entered, such as `/etc/sysconfig/network-scripts/ifcfg-ATT`. That file contains options that are passed to the `pppd` daemon for features that are negotiated with the remote PPP server.