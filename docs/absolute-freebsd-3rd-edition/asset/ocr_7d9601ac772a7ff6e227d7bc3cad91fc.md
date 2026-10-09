The packaging system is now installed. To smooth things out, the stub pkg(8) that ships with FreeBSD tells the newly installed packaging system to install the program you really wanted. In this case, our new pkg(8) installs mtimeofday for you.

You can install the packaging system on its own, without adding other packages, by running `pkg bootstrap` — but seriously, nobody does that at the command line. Running `pkg bootstrap` does nothing when the packaging system is already installed, so it’s useful for setup scripts.

# **Common pkg Options**

While each `pkg` subcommand has unique features, a few command options work across almost all of them.

In its default configuration, `pkg` prompts you for confirmation before doing anything. Tell `pkg` to take action without prompting you with the `-y` flag.

On the other hand, maybe you want `pkg` to show you what it would do if you ran a command, but not actually do anything. Perform a dry run by using the `-n` flag. For example, a package install using `-n` would show the names of every package to be installed, including dependencies. There’s no risk that the system would install the packages, however. Dry runs can help you prepare for changes during a maintenance window.

Many `pkg` operations produce a bunch of output. Reduce the amount of output with `-q`.

The `-a` flag usually applies a command to all installed packages.

Finally, `pkg` usually refuses to do pointless things or things that damage the system. The `-f` flag forces `pkg` to do what you said. Forcing package activities is usually, but not always, a bad idea. For example, you might need `-f` to forcibly reinstall a damaged package.

# **Configuring pkg(8)**

The `pkg(8)` program is designed to be highly flexible. While each subcommand has a whole bunch of options, you can establish