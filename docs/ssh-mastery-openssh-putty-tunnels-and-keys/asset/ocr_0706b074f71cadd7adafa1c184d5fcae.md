version: permit-agent-forwarding, permit-port-forwarding, permit-pty, permit-user-rc, and permit-x11-forwarding. Additionally you have the source-address restriction that dictates the IP addresses that can authenticate using this certificate. There’s also the clear restriction that (much like restrict in authorized_keys) turns off all privileges, allowing you to turn them on selectively with a permit- statement. Finally, force-command compels the user to run that specific command.

One common case for automation is when you have a key that can only run a single task. I want to create a certificate for a key that can only be used to run the command /usr/local/scripts/backup.sh. Create a key called backup on the client, and send backup.pub to the CA for signing. I want to erase all permissions from this certificate using the clear option, and then compel running the backup script with force-command. I use -O twice to assign these permissions. Otherwise, it looks like any other user key signing.

```
# ssh-keygen -s user-mwlca-key -I user_backup -n backup -V +52w -O clear -O force-command="/usr/local/scripts/backup.sh" backup.pub
```

This generates the certificate file backup-cert.pub. Look at the contents.

```
# ssh-keygen -Lf backup-cert.pub
backup-cert.pub:
    Type: ssh-rsa-cert-v01@openssh.com user certificate
    Public key: RSA-CERT SHA256:UL4ctioc5p8aSN1S318FI5RpsS1rnxJdr0EDb/B69Jg
    Signing CA: RSA SHA256:CKZFZXRg0y1ji8zmUhU0zjJQfNs9gLEqAWsJ8aP8B4dg
    Key ID: "user_backup"
    Serial: 0
    Valid: from 2017-12-05T07:56:00 to 2018-12-04T07:57:50
    Principals:
        backup
    Critical Options:
        force-command /usr/local/scripts/backup.sh
    Extensions: (none)
```

Compare this key to the regular user certificate we just created. The user key has no critical options, while this certificate lists the force-command statement as a critical option. Where the user key has a bunch of privileges under Extension, this key has none. This certificate grants the right to use only the one command.

There is no specific privilege to create an SSH tunnel at this time. If your organization is large enough to need certificates, it should have standards declaring acceptable VPN types.³

# Disabling authorized_keys

Once you’ve fully deployed SSH certificates for user authentication, you might decide to disable authorized_keys files. That’s easily done in sshd_config.

```
AuthorizedKeysFile none
```

If you have clients that can’t support certificates, however, you’ll need to provide a way for those clients to log in. Some organizations require all sysadmins to use Unix-based desktops so they can support certificates. Some large organizations like Facebook disallow SSH from clients except to a central