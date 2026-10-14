# Linux Users Are Not HA Users

The desire of Minerva to have its own ecosystem, with distinct usernames and passwords, is not egomanical for the sake of it; it’s merely a case of practicality because not everyone using the system will have (or should be able to get) a Linux-based account. After all, you want users to control the system through means that can be more easily authenticated on a fine-grained level. This gives you a multistage approach:

+   - Everyone living in the house or a family relative has a Minerva account. This gives you the option of allowing them to view family photos, see what you’re listening to, and so on. It also means they can use your services to retrieve shows from the TV guide or view the weather report.
+   - Everyone living in the house will generally also have a web username, which should match their Minerva user, to provide them access to this input conduit. They will be a subset of total Minerva users. This allows them to control their music selection and review certain house stats. Each web user has controllable read and write authentication to the various facilities.
+   - Most people living in the house will have access to the other input conduits, such as SMS or e-mail.
+   - Few users, usually just one, will have a Linux account allowing them to directly control the filesystem and users. A guest account will usually exist to allow read-only access to the Samba file servers so that music can be played locally. Other users will be created for the purpose of e-mailing light switches, for example, but will be made inaccessible to other dwellers by setting the shell to /bin/false.

Therefore, you will introduce your own read-only hierarchy within the Minerva filesystem (all relative to $MINBASE) covering each user, the applications, and their appropriate rights. The passwords for each input conduit will not be included here because the files must be publicly readable for the various commands to work. Instead, you rely on the input conduit (such as the web browser) to store its own passwords and validate the user. After all, you’re more likely to trust the experience of Apache in providing robust username security than yourself.

First you can add users to the system with a line such as this:

```
addminervauser steev "Steven Goodwin"
```

This will create a directory for them, beginning here:

```
$MINBASE/etc/users/steev
```

to hold all the user-specific settings and data, including the following:

+   - Full name
+   - Personal address book
+   - Default Minerva preferences (such as preferred style of synthetic voice)
+   - Access rights to various devices
+   - TV search terms
+   - External account references (such as links to their Google calendar)

Each application in the system has a specific code (home device, cdplayer, and so on) and an associated directory that holds files for determining the access rights such as r (for read-access) or rw (for read-write). I use r and rw as standard terms, even though their meaning isn’t directly analogous because, in the case of the CD player, read access