offered by the server. If you're really interested in tweaking your client's behavior, read ssh_config(5).

To connect to another host with SSH, type ssh hostname. In response, you'll see something like this:

```
# ssh mwl.io
The authenticity of host 'mwl.io (203.0.113.221)' can't be established.
ECDSA key fingerprint is SHA256:Zx0WgIg4oqqZKHOLV5tfgP1aWDW6UGViTvjfAjMc4E.
No matching host key fingerprint found in DNS.
Are you sure you want to continue connecting (yes/no)? **yes**
```

Your client immediately retrieves the public key from the host you're connecting to and checks its own internal list of SSH keys for a matching key for that host. If the key offered by the server matches the key the client has in its list, the client assumes you're talking to the correct host. If the client doesn't have the host key in its list of known hosts, it presents the key fingerprint for your approval.

The fingerprint presented by the SSH client should be identical to the fingerprint you generated on your server. If the fingerprint isn't identical, you're connecting to the wrong host and you need to immediately disconnect. If it matches, accept the key and continue. Once you accept the fingerprint, the key is saved under your home directory in .ssh/known_hosts.

If you're building a new server on your local network for your private use, perhaps you don't have to manually compare the key fingerprints. You should still copy the key fingerprint, however, since you'll eventually want to connect from a remote location and will need to verify the key. If many people will connect to a server, it's generally okay to put the fingerprint on a web page. You must decide how much security you need. I strongly encourage you to err on the side of caution.

Accept the host key, and you'll be allowed to log into the server. While using a private key with a passphrase is preferable to using passwords, a password with SSH is still better than telnet.

# ## Copying Files over SSH