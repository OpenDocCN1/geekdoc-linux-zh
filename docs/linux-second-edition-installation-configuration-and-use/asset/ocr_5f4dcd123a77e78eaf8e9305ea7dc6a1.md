A new command is provided for terminating an Emacs client: `Ctrl-X X`, ` #`. `Ctrl-C` must not be used since it would also terminate the Emacs server.

In order to have the Emacs client automatically called by various programs, you must preset the EDITOR and VISUAL environment variables in `/etc/profile` or `~/.profile` to emacsclient.

Some programs have to be configured individually in order to call the Emacs client for editing files. In the email program pine, for example, the following line must be changed in `~/.pinerc`. Emacs can now be called with `Ctrl+C` for writing email messages. Analogous configuration steps are possible for many other programs.

```
 # in "~/.pinerc"
editor=emacsclient
```