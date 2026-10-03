data and deleting your log files.

# Developing Automation Scripts

One challenge in restricting a key is understanding what commands the program actually needs, versus what you think it needs. The debugging mode of `sshd` can help you figure this out. Have your client run its command against `sshd` in debugging mode, and study the output. You’ll see all of the commands that the client runs. This will also let you lock down the key further than you might otherwise—if you know the exact flags rsync will use on your server, you can impose those as a restriction.

I’ve written scripts that seem to work from the command line, but fail when scheduled, and each time it’s turned out that my script was picking up authentication information from my SSH agent rather than using the key I’d created for the task. The IdentitiesOnly keyword tells ssh(1) to only use the identity specified on the command line and not your agent. Set -o `IdentitiesOnly=yes` in your script’s SSH command.

An automated script should never be prompted for user input. You don’t want your script hanging and waiting at a password prompt. The BatchMode keyword disables password and passphrase prompts. By setting BatchMode to `yes` the SSH part of your script will crash and die immediately, rather than pointlessly hanging around forever.

# Server-Side Restrictions

Perhaps you don’t want to use `authorized_keys` to restrict access, or maybe you’d like additional protections. You can use the ForceCommand `sshd_config` keyword to restrict what an account can run.

ForceCommand takes one argument, the command to be run. It’s run under the user’s regular privileges, and disregards whatever command the client requested. Much like defining a command in `authorized_keys`, ForceCommand retains the requested command in the `$SSH_ORIGINAL_COMMAND` environment variable.

ForceCommand is best used inside a Match statement.

# Automation and Root Logins

“My command needs to run as root!” It is possible to login as root using the PermitRootLogin keyword. Don’t do it. Logging in as root for automation breaks many fundamental security principles. Trusting your automated scripts with remote root privileges is a good way to spend an unscheduled weekend restoring the servers from backup. (You do have backups beyond rsync, right? Remember that rsync is a tactic, not a strategy.)

Yes, a few environments can securely support root logins. Some people are using root logins in a manner that can support auditing. If you’re reading this