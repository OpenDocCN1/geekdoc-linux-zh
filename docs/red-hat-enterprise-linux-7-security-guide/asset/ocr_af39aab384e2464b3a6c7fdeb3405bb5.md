# 4.10.1. Deploying a Tang server

To install the tang package and its dependencies, enter the following command as root:

```
```
~]# yum install tang
```
```

Enable and start the tangd service using systemd:

```
```
~]# systemctl enable tangd.socket --now
Created symlink from /etc/systemd/system/multi-
user.target.wants/tangd.socket to /usr/lib/systemd/system/tangd.socket.
```
```

Since tangd uses the systemd socket activation mechanism, the server starts as soon as the first connection comes in. A new set of cryptographic keys is automatically generated at the first start.

To perform cryptographic operations such as manual key generation, use the jose utility. Enter the jose -h command or see the jose(1) man pages for more information.

# Example 4.4. Rotating Tang Keys

It is important to periodically rotate your keys. The precise interval at which you should rotate them depends upon your application, key sizes, and institutional policy. For some common recommendations, see the Cryptographic Key Length Recommendation page.

To rotate keys, start with the generation of new keys in the key database directory, typically /var/db/tang. For example, you can create new signature and exchange keys with the following commands:

```
```
~]# DB=/var/db/tang
~]# jose jwk gen -i '{"alg":"ES512"}' -o $DB/new_sig.jwk
~]# jose jwk gen -i '{"alg":"ECMR"}' -o $DB/new_exc.jwk
```
```

Rename the old keys to have a leading . to hide them from advertisement. Note that the file names in the following example differs from real and unique file names in the key database directory.

```
```
~]# mv $DB/old_sig.jwk $DB/.old_sig.jwk
~]# mv $DB/old_exc.jwk $DB/.old_exc.jwk
```
```

Tang immediately picks up all changes. No restart is required.

At this point, new client bindings pick up the new keys and old clients can continue to utilize the old keys. When you are sure that all old clients use the new keys, you can remove the old keys.

![](bbox=[0.11, 0.81, 0.18, 0.88])

# WARNING

Be aware that removing the old keys while clients are still using them can result in data loss.