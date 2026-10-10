The `log.nmb` and `log.smb` files report status and error conditions for the `nmbd` and `smbd` servers, respectively. Additionally, whenever any errors are reported for any connecting client host (such as authentication failures), these messages are printed into a `log.<name>` file for that client. Note that this can result in a lot of files cluttering up your `/var/log` directory. You can switch to a combined log format by commenting out the `log file` line in `smb.conf`:

```
```
# this tells Samba to use a separate log file for each machine
# that connects
;	log file = /var/log/log.%m
```
```

SMB errors for individual hosts will go into `log.smb` with this line commented out.

Another useful line to modify is the `max log size` line, which is set to `50KB` by default. This control allows you to set the “rollover” size for any of the log files. When any Samba log file reaches the size you've designated, the file's renamed by appending `.old` to the filename, and new log entries are added to a new file. The `.old` file is overwritten at the next rollover.

```
```
# Put a capping on the size of the log files (in Kb).
	max log size = 50
```
```

# ## Samba Variables

Configuration parameters in `smb.conf` don't have to be hard-wired. You have a number of variable substitutions at your disposal, so you can set certain options to be dynamically determined, depending on the conditions of the connection. For example, you can set an option to reflect the client's username with the `%u` variable, allowing you to set a parameter such as `path = /usr/local/share/user-files/%u`. The user `harris` would thus receive the path `/usr/local/share/user-files/harris`.

Here are a few of the most useful variables:

+   - `%u`—The client's username.
+   - `%g`—The primary group name of `%u`.
+   - `%S`—The name of the current service, if any.
+   - `%H`—The home directory of the user given by `%u`.
+   - `%h`—The Internet hostname of the Samba server.
+   - `%M`—The Internet hostname of the client machine.
+   - `%L`—The NetBIOS name of the Samba server. This allows you to change your config based on what the client calls you; your server can have a “dual personality.”
+   - `%m`—The NetBIOS name of the client machine.
+   - `%I`—The IP address of the client machine.