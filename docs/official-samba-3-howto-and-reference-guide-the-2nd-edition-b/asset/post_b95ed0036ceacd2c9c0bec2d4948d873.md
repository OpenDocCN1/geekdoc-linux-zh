
### client NTLMv2 auth
This parameter determines whether or not smbclient(8) will attempt to authenticate itself to servers using the NTLMv2 encrypted password response.

If enabled, only an NTLMv2 and LMv2 response (both much more secure than earlier versions) will be sent. Many servers (including NT4 SP4, Win9x and Samba 2.2) are not compatible with NTLMv2.

Similarly, if enabled, **NTLMv1**, **client lanman auth** and **client plaintext auth** authentication will be disabled. This also disables share-level authentication.

If disabled, an NTLM response (and possibly a LANMAN response) will be sent by the client, depending on the value of **client lanman auth**.

Note that some sites (particularly those following ‘best practice’ security policies) only allow NTLMv2 responses, and not the weaker LM or NTLM.

### client plaintext auth **(G)**
Default: *client plaintext auth* = *yes*

Specifies whether a client should send a plaintext password if the server does not support encrypted passwords.

### client schannel **(G)**
Default: *client schannel* = *auto*

Example: *client schannel* = *yes*

This controls whether the client offers or even demands the use of the netlogon channel. *client schannel* = *no* does not offer the channel, *client schannel* = *auto* offers the channel but does not enforce it, and *client schannel* = *yes* denies access if the server is not able to speak netlogon channel.

### client signing **(G)**
Default: *client signing* = *auto*

This controls whether the client offers or requires the server it talks to to use SMB signing. Possible values are *auto*, *mandatory* and *disabled*.

When set to auto, SMB signing is offered, but not enforced. When set to mandatory, SMB signing is required and if set to disabled, SMB signing is not offered either.

### client use spnego **(G)**
Default: *client use spnego* = *yes*

This variable controls whether Samba clients will try to use Simple and Protected NEGociation (as specified by rfc2478) with supporting servers (including Windows XP, Windows 2000 and Samba 3.0) to agree upon an authentication mechanism. This enables Kerberos authentication in particular.

### comment **(S)**
Default: *comment* = *No comment*

Example: *comment* = *Fred’s Files*

This is a text field that is seen next to a share when a client queries the server, either via the network neighborhood or via **net view** to list what shares are available. If you want to set the string that is displayed next to the machine name then see the *server string* parameter.

### config file **(G)**
Default: *No default*

Example: *config file = /usr/local/samba/lib/smb.conf.%m*

This allows you to override the config file to use, instead of the default (usually *smb.conf*). There is a chicken and egg problem here as this option is set in the config file!

For this reason, if the name of the config file has changed when the parameters are loaded then it will reload them from the new config file.

This option takes the usual substitutions, which can be very useful.

If the config file doesn't exist then it won't be loaded (allowing you to special case the config files of just a few clients).

### copy **(S)**
Default: *No default*

Example: *copy = otherservice*

This parameter allows you to "clone" service entries. The specified service is simply duplicated under the current service's name. Any parameters specified in the current section will override those in the section being copied.

This feature lets you set up a 'template' service and create similar services easily. Note that the service being copied must occur earlier in the configuration file than the service doing the copying.

### create mode
This parameter is a synonym for *create mask*.

### create mask **(S)**
Default: *create mask = 07440755*

Example: *create mask = 0775*

When a file is created, the necessary permissions are calculated according to the mapping from DOS modes to UNIX permissions, and the resulting UNIX mode is then bit-wise 'AND'ed with this parameter. This parameter may be thought of as a bit-wise MASK for the UNIX modes of a file. Any bit *not* set here will be removed from the modes set on a file when it is created.

The default value of this parameter removes the *group* and *other* write and execute bits from the UNIX modes.

Following this Samba will bit-wise 'OR' the UNIX mode created from this parameter with the value of the *force create mode* parameter which is set to *000* by default.

This parameter does not affect directory masks. See the parameter `directory mask` for details.

Note that this parameter does not apply to permissions set by Windows NT/2000 ACL editors. If the administrator wishes to enforce a mask on access control lists also, they need to set the `security mask`.

### csc policy **(S)**
Default: `csc policy = manual`

Example: `csc policy = programs`

This stands for `client-side caching policy`, and specifies how clients capable of offline-caching will cache the files in the share. The valid values are: manual, documents, programs, disable.

These values correspond to those used on Windows servers.

For example, shares containing roaming profiles can have offline caching disabled using `csc policy = disable`.

### cups options **(S)**
Default: `cups options = "raw,media=a4,job-sheets=secret,secret"`

Example: `cups options = "raw,media=a4,job-sheets=secret,secret"`

This parameter is only applicable if `printing` is set to `cups`. Its value is a free form string of options passed directly to the cups library.

You can pass any generic print option known to CUPS (as listed in the CUPS “Software Users’ Manual”). You can also pass any printer specific option (as listed in `loptions -d printername -I`) valid for the target queue.

You should set this parameter to `raw` if your CUPS server `error_log` file contains messages such as “Unsupported format \ application/octet-stream” when printing from a Windows client through Samba. It is no longer necessary to enable system wide raw printing in `/etc/cups/mime.{conv,types}`.

### cups server **(G)**
Default: `cups server = MYCUPSSERVER`

Example: `cups server = MYCUPSSERVER`

This parameter is only applicable if `printing` is set to `cups`.

If set, this option overrides the ServerName option in the CUPS `client.conf`. This is necessary if you have virtual samba servers that connect to different CUPS daemons.

### deadtime **(G)**
Default: `deadtime = 0`

Example: `deadtime = 15`

The value of the parameter (a decimal integer) represents the number of minutes of inactivity before a connection is considered dead, and it is disconnected. The deadtime only takes effect if the number of open files is zero.

This is useful to stop a server’s resources being exhausted by a large number of inactive connections.

Most clients have an auto-reconnect feature when a connection is broken so in most cases this parameter should be transparent to users.

Using this parameter with a timeout of a few minutes is recommended for most systems.

A deadtime of zero indicates that no auto-disconnection should be performed.

### debug hires timestamp **(G)**
Default: *debug hires timestamp = no*

Sometimes the timestamps in the log messages are needed with a resolution of higher than seconds, this boolean parameter adds microsecond resolution to the timestamp message header when turned on.

Note that the parameter *debug timestamp* must be on for this to have an effect.

### debug pid **(G)**
Default: *debug pid = no*

When using only one log file for more then one forked smbd(8)-process there may be hard to follow which process outputs which message. This boolean parameter adds the process-id to the timestamp message headers in the logfile when turned on.

Note that the parameter *debug timestamp* must be on for this to have an effect.

### timestamp logs
This parameter is a synonym for *debug timestamp*.

### debug timestamp **(G)**
Default: *debug timestamp = yes*

Samba debug log messages are timestamped by default. If you are running at a high *debug level* these timestamps can be distracting. This boolean parameter allows timestamping to be turned off.

### debug uid **(G)**
Default: *debug uid = no*

Samba is sometimes run as root and sometime run as the connected user, this boolean parameter inserts the current euid, egid, uid and gid to the timestamp message headers in the log file if turned on.

Note that the parameter *debug timestamp* must be on for this to have an effect.

### default case **(S)**
Default: *default case = lower*

See the section on *name mangling*. Also note the *short preserve case* parameter.

### default devmode **(S)**
Default: *default devmode = no*
