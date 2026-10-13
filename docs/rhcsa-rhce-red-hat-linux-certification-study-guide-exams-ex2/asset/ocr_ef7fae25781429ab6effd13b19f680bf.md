In contrast, the following command excludes the paps and the gutenprint-cups packages from the list of those to be installed:

```
# yum groupinstall "Print Server" -x paps -x gutenprint-cups
```

The options to the yum command are not complete unless there's a command that can reverse the process. As suggested by the name, the groupremove option uninstalls all packages from the noted package group:

```
# yum groupremove "Print Server"
```

Exclusions are not possible with the groupremove switch. If you don't want to remove all packages listed in the output to the command, it may be best to remove target packages individually.

# More yum Commands

A number of additional yum-related commands are available. Two of them may be of particular interest to those studying for the Red Hat exams: yum-config-manager and yumdownloader, which can display all current settings for each repository as well as download individual RPM packages. One more related command is createrepo, which can help you set up a local repository.

# View All Directives with yum-config-manager

To some extent, the directives listed in the yum.conf and related configuration files provide only a small snapshot of available directives. To review the full list of directives, run the yum-config-manager command. Pipe it to the less command as a pager. It includes 100 lines. The excerpt from the [main] repository shown in Figure 7-12 is based on the connection to the RHN.

Many of the directives associated with yum are not filled in, such as assumeyes; some don't really matter, such as the color directives. Some of the other significant directives are shown in Table 7-5. It is not a comprehensive list. If you're interested in a directive not shown, it's defined in the man page for the yum.conf file.

# Package Downloads with yumdownloader

As suggested by the name, the yumdownloader command can be used to download packages from yum-based repositories. It's a fairly simple command. For example, the