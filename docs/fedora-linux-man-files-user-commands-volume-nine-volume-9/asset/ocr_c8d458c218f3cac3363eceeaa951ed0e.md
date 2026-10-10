# ENVIRONMENT VARIABLES

The PulseAudio client libraries check for the existence of the following environment variables and change their local configuration accordingly:

*$PULSE_SERVER*: the server string specifying the server to connect to when a client asks for a sound server connection and doesn't explicitly ask for a specific server. The server string is a list of server addresses separated by whitespace which are tried in turn. A server address consists of an optional address type specifier (unix:, tcp:, tcp4:, tcp6:), followed by a path or host address. A host address may include an optional port number. A server address may be prefixed by a string enclosed in { }. In this case the following server address is ignored unless the prefix string equals the local hostname or the machine ID (//etc/machine-id).

*$PULSE_SINK*: the symbolic name of the sink to connect to when a client creates a playback stream and doesn't explicitly ask for a specific sink.

*$PULSE_SOURCE*: the symbolic name of the source to connect to when a client creates a record stream and doesn't explicitly ask for a specific source.

*$PULSE_BINARY*: path of PulseAudio executable to run when server auto-spawning is used.

*$PULSE_CLIENTCONFIG*: path of file that shall be read instead of *client.conf* (see above) for client configuration.

*$PULSE_COOKIE*: path of file that contains the PulseAudio authentication cookie. Defaults to *~/config/pulse/cookie*.

These environment settings take precedence — if set — over the configuration settings from *client.conf* (see above).