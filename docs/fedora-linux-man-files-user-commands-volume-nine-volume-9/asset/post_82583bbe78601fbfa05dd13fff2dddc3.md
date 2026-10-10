

# ENVIRONMENT

**DISPLAY and SSH_ASKPASS**

If **ssh-add** needs a passphrase, it will read the passphrase from the current terminal if it was run from a terminal. If **ssh-add** does not have a terminal associated with it but **DISPLAY** and **SSH_ASKPASS** are set, it will execute the program specified by **SSH_ASKPASS** (by default “ssh-askpass”) and open an X11 window to read the passphrase. This is particularly useful when calling **ssh-add** from a .xsession or related script. (Note that on some machines it may be necessary to redirect the input from /dev/null to make this work.)

**SSH_AUTH_SOCK**

Identifies the path of a UNIX socket used to communicate with the agent.

**SSH_USE_STRONG_RNG**

The reseeding of the OpenSSL random generator is usually done from **/dev/urandom**.

If the **SSH_USE_STRONG_RNG** environment variable is set to a value other than **0**, the OpenSSL random generator is reseeded from **/dev/random**. The number of bytes read is defined by the **SSH_USE_STRONG_RNG** value. Minimum is 14 bytes. This setting is not recommended on the computers without the hardware random generator because insufficient entropy causes the connection to be blocked until enough entropy is available.

# FILES

- `~/ssh/identity`
  - Contains the protocol version 1 RSA authentication identity of the user.
- `~/ssh/id_dsa`
  - Contains the protocol version 2 DSA authentication identity of the user.
- `~/ssh/id_ecdsa`
  - Contains the protocol version 2 ECDSA authentication identity of the user.
- `~/ssh/id_ed25519`
  - Contains the protocol version 2 Ed25519 authentication identity of the user.
- `~/ssh/id_rsa`
  - Contains the protocol version 2 RSA authentication identity of the user.

Identity files should not be readable by anyone but the user. Note that ssh-add ignores identity files if they are accessible by others.

# EXIT STATUS

Exit status is 0 on success, 1 if the specified command fails, and 2 if **ssh-add** is unable to contact the authentication agent.

# SEE ALSO

ssh(1), ssh-agent(1), ssh-askpass(1), ssh-keygen(1), sshd_config(5)

# AUTHORS

OpenSSH is a derivative of the original and free ssh 1.2.12 release by Tatu Ylonen. Aaron Campbell, Bob Beck, Markus Friedl, Niels Provos, Theo de Raadt and Dug Song removed many bugs, re-added newer features and created OpenSSH. Markus Friedl contributed the support for SSH protocol versions 1.5 and 2.0.

# SSH-AGENT

## NAME

**ssh-agent** - authentication agent

## SYNOPSIS

```
ssh-agent [ -c | s ] [ -a bind_address ] [ -E fingerprint_hash ] [ -t life ] [ command [arg ... ] ]
ssh-agent [ -c | s ] -k
```

## DESCRIPTION

**ssh-agent** is a program to hold private keys used for public key authentication (RSA, DSA, ECDSA, Ed25519). **ssh-agent** is usually started in the beginning of an X-session or a login session, and all other windows or programs are started as clients to the ssh-agent program. Through use of environment variables the agent can be located and automatically used for authentication when logging in to other machines using ssh(1).

The agent initially does not have any private keys. Keys are added using ssh-add(1). multiple identities may be stored in **ssh-agent** concurrently and ssh(1) will automatically use them if present. ssh-add(1) is also used to remove keys from **ssh-agent** and to query the keys that are held in one.

The options are as follows:

- `-a` *bind_address*
  - Bind the agent to the UNIX socket *bind_address*. The default is `$TMPDIR/ssh-XXXXXXXXXX/agent.<pid>`.
- `-c`
  - Generate C-shell commands on **stdout**. This is the default if **SHELL** looks like it’s a csh style of shell.
- `-D`
  - Foreground mode. When this option is specified **ssh-agent** will not fork.
- `-d`
  - Debug mode. When this option is specified **ssh-agent** will not fork and will write debug information to standard error.
- `-E` *fingerprint_hash*
  - Specifies the hash algorithm used when displaying key fingerprints. Valid options are: “md5” and “sha256”. The default is “sha256”.
- `-k`
  - Kill the current agent (given by the **SSH_AGENT_PID** environment variable).
- `-s`
  - Generate Bourne shell commands on **stdout**. This is the default if **SHELL** does not look like it’s a csh style of shell.
- `-t` *life*
  - Set a default value for the maximum lifetime of identities added to the agent. The lifetime may be specified in seconds or in a time format specified in sshd_config(5). A lifetime specified for an identity with ssh-add(1) overrides this value. Without this option the default maximum lifetime is forever.

If a command line is given, this is executed as a subprocess of the agent. When the command dies, so does the agent.

The idea is that the agent is run in the user’s local PC, laptop, or terminal. Authentication data need not be stored on any other machine, and authentication passphrases never go over the network. However, the connection to the agent is forwarded over SSH remote login, and the user can thus use the privileges given by the identities anywhere in the network in a secure way.

There are two main ways to get an agent set up: The first is that the agent starts a new subcommand into which some environment variables are exported, eg **ssh-agent xterm &**. The second is that the agent prints the needed shell commands (either sh(1) or csh(1) syntax can be generated) which can be evaluated in the calling shell, eg `eval ‘ssh-agent -s’` for Bourne-type shells such as sh(1) and bash(1) and `eval ‘ssh-agent -c’` for csh(1) and derivatives.

Later ssh(1) looks at these variables and uses them to establish a connection to the agent.

The agent will never send a private key over its request channel. Instead, operations that require a private key will be performed by the agent, and the result will be returned to the requester. This way, private keys are not exposed to clients using the agent.

A UNIX socket is created and the name of this socket is stored in the **SSH_AUTH_SOCK** environment variable. The socket is made accessible only to the current user. This method is easily abused by root or another instance of the same user.

The **SSH_AGENT_PID** environment variable holds the agent’s process ID.

The agent exits automatically when the command given on the command line terminates.

## FILES

**$TMPDIR/ssh-XXXXXXXXXX/agent.<pid>**

UNIX sockets used to contain the connection to the authentication agent. These sockets should only be readable by the owner. The sockets should get automatically removed when the agent exits.

## ENVIRONMENT

### SSH_USE_STRONG_RNG

The reseeding of the OpenSSL random generator is usually done from **/dev/urandom**. If the **SSH_USE_STRONG_RNG** environment variable is set to a value other than **0**, the OpenSSL random generator is reseeded from **/dev/random**. The number of bytes read is defined by the SSH_USE_STRONG_RNG value. Minimum is 14 bytes. This setting is not recommended on the computers without the hardware random generator because insufficient entropy causes the connection to be blocked until enough entropy is available.

## SEE ALSO

ssh(1), ssh-add(1), ssh-keygen(1), sshd(8)

## AUTHORS

OpenSSH is a derivative of the original and free ssh 1.2.12 release by Tatu Ylonen. Aaron Campbell, Bob Beck, Markus Friedl, Niels Provos, Theo de Raadt and Dug Song removed many bugs, re-added newer features and created OpenSSH. Markus Friedl contributed the support for SSH protocol versions 1.5 and 2.0.

# SSH-COPY-ID

## NAME

ssh-copy-id - use locally available keys to authorise logins on a remote machine

## SYNOPSIS

```
ssh-copy-id [ -n ] [ -i [ identity_file ] ] [ -p port ] [ -o ssh_option ] [ user @ ] hostname -h |-v
```

## DESCRIPTION

ssh-copy-id is a script that uses ssh(1) to log into a remote machine (presumably using a login password, so password authentication should be enabled, unless you’ve done so clever use of multiple identities). It assesses a list of one or more fingerprints (as described below) and tries to log in with each key, to see if any of them are already installed (of course, if you are not using ssh-agent(1) this may result in you being repeatedly prompted for pass-phrases). It then assesses a list of those that failed to log in, and using ssh, enables logins with those keys on the remote server. By default it adds the keys by appending them to the remote user’s `~/.ssh/authorized_keys` (creating the file, and directory, if necessary). It is also capable of detecting if the remote system is a NetScreen, and using its ‘set’ ssh pka key ... command instead.

The options are as follows:

- `-i identity_file`
  - Use only the key(s) contained in *identity_file* (rather than looking for identities via ssh-add(1) or in the **default_ID_file**). If the filename does not end in .pub this is added. If the filename is omitted, the **default_ID_file** is used.
  - Note that this can be used to ensure that the keys copied have the comment one prefers and/or extra options applied, by ensuring that the key file has these set as preferred before the copy is attempted.
- `-n`
  - Do a dry-run. Instead of installing keys on the remote system simply prints the key(s) that would have been installed.
- `-h, -v`
  - Print Usage summary
- `-P port , -o ssh_option`
  - These two options are simply passed through untouched, along with their argument, to allow one to set the port or other ssh(1) options, respectively.
  - Rather than specifying these as command line options, it is often better to use (per-host) settings in ssh(1)’s configuration file: ssh_config(5).

Default behaviour without -i is to check if ‘ssh-add’ -L provides any output, and if so those keys are used. Note that this results in the comment on the key being the filename that was given to ssh-add(1) when the key was loaded into your ssh-agent(1) rather than the comment contained in that file, which is a bit of a shame. Otherwise, if ssh-add(1) provides no keys contents of the **default_ID_file** will be used.

The **default_ID_file** is the most recent file that matches: `~/.ssh/id*.pub` (excluding those that match `~/.ssh/*-cert.pub`). So if you create a key that is not the one you want to use, just use `touch(1)` on your preferred key’s .pub file to reinstate it as the most recent.

