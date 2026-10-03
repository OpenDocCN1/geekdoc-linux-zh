# Linux Hack

# Three Minor Annoyances of ssh-copy-id

Ajay Kumar Tiwari

Following are few minor annoyances of the ssh-copy-id.

+   1. Default public key: ssh-copy-id uses ~/.ssh/identity.pub as the default public key file (i.e when no value is passed to option -i). Instead, I wish it uses id_dsa.pub, or id_rsa.pub, or identity.pub as default keys. i.e If any one of them exist, it should copy that to the remote-host. If two or three of them exist, it should copy identity.pub as default.
2. The agent has no identities: When the ssh-agent is running and the ssh-add -L returns “The agent has no identities” (i.e no keys are added to the ssh-agent), the ssh-copy-id will still copy the message “The agent has no identities” to the remote-host’s authorized_keys entry.
3. Duplicate entry in authorized_keys: I wish ssh-copy-id validates duplicate entry on the remote-host’s authorized_keys. If you execute ssh-copy-id multiple times on the local-host, it will keep appending the same key on the remote-host’s authorized_keys file without checking for duplicates. Even with duplicate entries everything works as expected. But, I would like to have my authorized_keys file clutter free.

# Hack 74. Crontab

Using cron you can execute a shell-script or Linux commands at a specific time and date. For example a sysadmin can schedule a backup job that can run every day.

How to add a job to the cron?

```
# crontab –e
0 5 * * * /root/bin/backup.sh
```