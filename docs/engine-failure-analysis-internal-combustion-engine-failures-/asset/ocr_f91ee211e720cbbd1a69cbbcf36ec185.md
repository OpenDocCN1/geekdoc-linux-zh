assign values to *positional parameters*. For example, if you specify a value for `argument 1`, bash assigns this value to `$1`. You can also use this command to choose *shell modes* for the current operating environment, including `noclobber`, which prevents bash from overwriting files when you use output redirection.

# OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| `--O` `shell` `mode` | Enable one of the following shell modes (`-o`) or disable a shell mode (`+o`). (The preceding is not a misprint; you use `--` to turn the option on and `++` to turn it off.) The following lists the available shell modes. The typical default settings are indicated in parentheses. |
| `+o` `shell` `mode` | `allexport` `(off)` Automatically export variables. |
| | `braceexpand` `(on)` Enable brace expansion. |
| | `emacs` `(on)` Use `emacs` as the default editor. |
| | `errexit` `(off)` Exit if a command encounters an error. |
| | `histexpand` `(on)` Enable history expansion. |
| | `ignoreeof` `(off)` Do not exit on end of file. |
| | `interactive-comments` `(on)` Treat `#` as a comment character. |
| | `monitor` `(on)` Enable job control. |
| | `noclobber` `(off)` Do not overwrite files when using output redirection. |
| | `noexec` `(off)` Do not execute commands. |
| | `noglob` `(off)` Do not use filename expansion. |
| | `noh` `(off)` Do not use command hashing. |
| | `notify` `(off)` Show message about background jobs at termination. |
| | `nunset` `(off)` Treat unset variables as errors in substitutions. |
| | `physical` `(off)` Print absolute path names in response to `pwd`. |
| | `posix` `(off)` Use POSIX standards. |
| | `privileged` `(off)` Start as the superuser; do not process the user's profile. |
| | `verbose` `(off)` Show each shell command when read. |
| | `vi` `(off)` Use `vi` as the default editor. |
| | `xtrace` `(off)` Show commands and arguments as they are executed. |