# Chapter 12 Software Installation and Management

```
$ sudo sh -c "echo mtab >> .gitignore" ^{10}$
```

Finally, we'll commit all the remaining changes:

```
$ sudo git add
$ sudo commit -m "Installed foobar; added RAID spare"
Created commit 329786e: Installed foobar; added RAID spare
4 files changed, 3 insertions(+), 1 deletion(-)
create mode 100644 .gitignore
create mode 100644 foobar/foobar.conf
delete mode 100644 mtab
```

Note that the gitfile becomes part of the managed set of files. It's fine to re-add files that are already under management, so git add is an easy way to say "I want to make the new repository image look like the current directory." You couldn't just do git commit -a in this situation that would pick up new foobar.conf nor .gitignore: these files are new to management by Git and must be explicitly added.

In an effort to fool you into thinking that it manages files' permissions as well as its contents, Git shows you when adding new files to the repository. It's lying. Git does not track moves, owners, or modifications. If you use Git to revert changes to system files, double-check that their attributes remain OK. A corollary is that you can't count on Git to recover complex file hierarchies from scratch in situations where the ownerships and permissions are important.

Using Git for basic version control isn't significantly more painful than making manual backup copies. The hard part is getting your administrative team to speed with the system and making sure it's used consistently.

# 12.10 SOFTWARE LOCALIZATION AND CONFIGURATION

Adapting computers to your local environment is one of the prime battlegrounds of system administration: tell the system about all the printers available on the network, start the special licensing daemon, the cron job that cleans the /scratch once a week, integrate support for that scanner they use over in the graphics department, and so on. Taking care of these issues in a structured and reproducible way is a central goal of architectural thinking.

Keep the following points in mind:

+   * Users do not have root privileges. Any need for root privileges in the course of normal operations is suspicious and probably indicates that something is fishy with your local configuration.
* Users do not wreck the system intentionally. Design internal security that guards against unintentional errors and the widespread dissemination of administrative privileges.

> 1 The explicit call to sh forces the redirection operator to be evaluated in the context of a root shell. If we simply type echo mtab >> .gitignore, the shell would try to open .gitignore before running sudo.