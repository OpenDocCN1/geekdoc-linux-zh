
# ENVIRONMENT VARIABLES

The PulseAudio client libraries check for the existence of the following environment variables and change their local configuration accordingly:

- **$PULSE_SERVER**: the server string specifying the server to connect to when a client asks for a sound server connection and doesn't explicitly ask for a specific server. The server string is a list of server addresses separated by whitespace which are tried in turn. A server address consists of an optional address type specifier (unix:, tcp:, tcp4:, tcp6:), followed by a path or host address. A host address may include an optional port number. A server address may be prefixed by a string enclosed in { }. In this case the following server address is ignored unless the prefix string equals the local hostname or the machine ID (//etc/machine-id).
- **$PULSE_SINK**: the symbolic name of the sink to connect to when a client creates a playback stream and doesn't explicitly ask for a specific sink.
- **$PULSE_SOURCE**: the symbolic name of the source to connect to when a client creates a record stream and doesn't explicitly ask for a specific source.
- **$PULSE_BINARY**: path of PulseAudio executable to run when server auto-spawning is used.
- **$PULSE_CLIENTCONFIG**: path of file that shall be read instead of *client.conf* (see above) for client configuration.
- **$PULSE_COOKIE**: path of file that contains the PulseAudio authentication cookie. Defaults to *~/config/pulse/cookie*.

These environment settings take precedence — if set — over the configuration settings from *client.conf* (see above).

# AUTHORS

The PulseAudio Developers <pulseaudio-discuss@lists.freedesktop.org>; PulseAudio is available from

# SEE ALSO

- (5), (5), (5), (1)

# PWD

## NAME

pwd - print name of current/working directory

## SYNOPSIS

**pwd** [*OPTION*]...

## DESCRIPTION

Print the full file name of the current working directory.

- **-L, —logical**
  use PWD from environment, even if it contains symlinks
- **-P, —physical**
  avoid all symlinks
- **—help**
  display this help and exit
- **—version**
  output version information and exit

If no option is specified, -P is assumed.

NOTE: your shell may have its own version of pwd, which usually supersedes the version described here. Please refer to your shell’s documentation for details about the options it supports.

# AUTHOR

Written by Jim Mayering.

# REPORTING BUGS

GNU coreutils online help: <> Report pwd translation bugs to <>

# COPYRIGHT

Copyright 2015 Free Software Foundation, Inc. License GPLv3+: GNU GPL version 3 or later <>. This is free software: you are free to change and redistribute it. There is NO WARRANTY, to the extent permitted by law.

# SEE ALSO

- (3)

Full documentation at: `<>` or available locally via: info ‘(coreutils) pwd invocation’

# PWMAKE

## NAME

pwmake - simple tool for generating random relatively easily pronounceable passwords

## SYNOPSIS

```
pwmake <entropy-bits>
```

## DESCRIPTION

**pwmake** is a simple configurable tool for generating random and relatively easily pronounceable passwords. The tool allows you to specify the number of entropy bits that are used to generate the password.

The entropy is pulled from /dev/urandom.

The minimum number of bits is 56 which is usable for passwords on systems/services where brute force attacks are of very limited rate of tries. The 64 bits should be adequate for applications where the attacker does not have direct access to the password hash file. For situations where the attacker might obtain the direct access to the password hash or the password is used as an encryption key 80 to 128 bits should be used depending on your level of paranoia.

## OPTIONS

The first and only argument is the number of bits of entropy used to generate the password.

## FILES

/etc/security/pwquality.conf - The configuration file for the libpwquality library.

## RETURN CODES

**pwmake** returns 0 on success, non zero on error.

## SEE ALSO

- (1), (8)

# AUTHORS

Tomas Mráz <>

# PWQCHECK

## NAME

**pwqcheck** - Check passphrase quality

## SYNOPSIS

*[options]*

## DESCRIPTION

The **pwqcheck** program checks passphrase quality using the libpasswdqc library. By default, it expects to read 3 lines from standard input:

- **first line is a new password,**
- **second line is an old password, and**
- **third line is either an existing account name or a**
  (5) entry.

There are a number of supported options, which can be used to control the **pwqcheck** behavior.

**pwqcheck** prints *OK* on success. Scripts invoking **pwqcheck** are suggested to check for both a zero exit status and the *OK* line.

## OPTIONS

**min = N0 , N1 , N2 , N3 , N4**
(default: min=disabled,24,11,8,7)

The minimum allowed password lengths for different kinds of passwords/passphrases. The keyword **disabled** can be used to disallow passwords of a given kind regardless of their length. Each subsequent number is required to be no larger than the preceding one.

*N0* is used for passwords consisting of characters from one character class only. The character classes are: digits, lower-case letters, upper-case letters, and other characters. There is also a special class for **non- ASCII** characters, which could not be classified, but are assumed to be non-digits.

*N1* is used for passwords consisting of characters from two character classes that do not get the requirements for a passphrase.

*N2* is used for passphrases. Note that besides setting this length requirement, a passphrase must also consist of a sufficient number of words (see the **passphrase** option below).

*N3* and *N4* are used for passwords consisting of characters from three and four character classes, respectively.

When calculating the number of character classes, upper-case letters used as the first character and digits used as the last character of a password are not counted.

In addition to being sufficiently long, passwords are required to contain enough different characters for the character classes and the minimum length they have been checked against.

**max = N**
(default: **max = 40** ) The maximum allowed password length. This can be used to prevent users from setting passwords that may be too long for some system services. The value 8 is treated specially: if **max** is set to 8, passwords longer than 8 characters will not be rejected, but will be truncated to 8 characters for the strength checks and the user will be warned. This is to be used with the traditional DES-based password hashes, which truncate the password at 8 characters.

It is important that you do set **max = 8** if you are using the traditional hashes, or so weak passwords will pass the checks.

**passphrase = N**
(default: **passphrase = 3** ) The number of words required for a passphrase.

**match = N**
(default: **match = 4** ) The length of common substring required to conclude that a password is at least partially based on information found in a character string, or 0 to disable the substring search. Note that the password will not be rejected once a weak substring is found; it will instead be subjected to the usual strength requirements with the weak substring partially discounted.

The substring search is case-insensitive and is able to detect and remove a common substring spelled backwards.

config = FILE

Load config *FILE* in the **passwdqc.conf** format. This file may define any options described in passwdqc.conf(5), but only the **min max passphrase match** , and **config** options are honored by .

- -1
  Read just 1 line (new passphrase). This is needed to use **pwqcheck** as the passwordcheck program on OpenBSD - e.g., with “:passwordcheck=/usr/bin/pwqcheck -1:” in the “default” section in /etc/login.conf
- -2
  Read just 2 lines (new and old passphrases).
- —Iti
  Check multiple passphrases (until EOF). This option may be used on its own or along with the *-1* or *-2* options. **pwqcheck** will read 1, 2, or 3 lines and will output one line per passphrase to check. The lines will start with either *OK* or a message explaining why the passphrase did not pass the checks, followed by a colon and a space, and finally followed by the passphrase. The explanatory message is guaranteed to not include a colon. With this option, the exit status of **pwqcheck** depends solely on whether there were any errors preventing the strength of passphrases from being fully checked or not. A primary use for this option is to test different policies and/or different versions of passwdqc on large passphrase lists.
- —version
  Output **pwqcheck** program version and exit.
- *-h* , —help
  Output **pwqcheck** help text and exit.
